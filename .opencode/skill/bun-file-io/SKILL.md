---
name: bun-file-io
description: 在进行文件操作时使用，如读取、写入、扫描或删除文件。总结了此代码库中首选的文件 API 和模式。还说明了何时使用文件系统辅助函数处理目录。
---

## 何时使用

- 编辑 `packages/opencode` 中的文件 I/O 或扫描
- 处理目录操作或外部工具

## Bun 文件 API（来自 Bun 文档）

- `Bun.file(path)` 是惰性的；调用 `text`、`json`、`stream`、`arrayBuffer`、`bytes`、`exists` 来读取。
- 元数据：`file.size`、`file.type`、`file.name`。
- `Bun.write(dest, input)` 写入字符串、缓冲区、Blobs、Responses 或文件。
- `Bun.file(...).delete()` 删除文件。
- `file.writer()` 返回 FileSink 用于增量写入。
- `Bun.Glob` + `Array.fromAsync(glob.scan({ cwd, absolute, onlyFiles, dot }))` 用于扫描。
- 使用 `Bun.which` 查找二进制文件，然后使用 `Bun.spawn` 运行它。
- `Bun.readableStreamToText/Bytes/JSON` 用于流输出。

## 何时使用 node:fs

- 使用 `node:fs/promises` 处理目录（`mkdir`、`readdir`、递归操作）。

## 代码库模式

- 优先使用 Bun API 而非 Node `fs` 进行文件访问。
- 读取前检查 `Bun.file(...).exists()`。
- 对于二进制/大文件使用 `arrayBuffer()` 并通过 `file.type` 检查 MIME。
- 使用 `Bun.Glob` + `Array.fromAsync` 进行扫描。
- 使用 `Bun.readableStreamToText` 解码工具 stderr。
- 对于大写入，使用 `Bun.write(Bun.file(path), text)`。

## 快速检查清单

- 优先使用 Bun API。
- 使用 `path.join`/`path.resolve` 处理路径。
- 尽可能优先使用 promise `.catch(...)` 而非 `try/catch`。
