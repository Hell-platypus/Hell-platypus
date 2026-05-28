# Ansible Loop 模块教学

## 快速运行

```bash
# 检查语法
ansible-playbook loop_tutorial.yml --syntax-check

# 执行（dry-run 安全模式，不会实际修改系统）
ansible-playbook -i inventory.yml loop_tutorial.yml -C

# 正式执行
ansible-playbook -i inventory.yml loop_tutorial.yml
```

> ⚠️ 注意：部分任务含有 `check_mode: yes` 或 `when: false`，仅作教学演示，不会真正写文件。

## 内容概览

| 序号 | 主题 | 说明 |
|------|------|------|
| 1 | 基础 loop | 直接写在 task 中遍历列表 |
| 2 | 遍历变量 | 引用 vars 中定义的列表 |
| 3 | 遍历字典列表 | 用 `item.key` / `item.value` 访问子字段 |
| 4 | index_var | 获取当前循环索引 |
| 5 | loop_var | 自定义循环变量名（替代默认的 `item`） |
| 6 | label | 美化 Ansible 输出显示 |
| 7 | with_items | 旧式循环语法（兼容） |
| 8 | loop + when | 循环中过滤/跳过元素 |
| 9 | dict2items | 遍历字典的键值对 |
| 10 | subelements | 嵌套循环遍历 |
| 11 | range | 生成数字序列 |
| 12 | until + retries | 重试机制 |
| 13-14 | 实战示例 | 批量创建用户 / 配置文件 |
| 15 | pause | 循环间暂停 |

## 核心要点

- **新版推荐使用 `loop`**（而非旧式的 `with_*`）
- 默认循环变量名是 `item`，可用 `loop_var` 自定义
- `loop_control` 提供索引、标签、暂停等控制能力
- `when` 可在循环中过滤元素
- `until` + `retries` 可实现重试逻辑
