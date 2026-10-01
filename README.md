# 产品知识库智能问答系统（RAG）

基于 FastAPI + ChromaDB + 通义千问 的本地知识库问答应用。

## 项目简介

本项目实现了一个完整的 RAG（检索增强生成）应用，能够根据本地产品知识库回答用户问题。  
支持知识库持久化存储和动态添加新文档。

### 主要功能

- 向量检索 + 大模型生成问答
- 知识库本地持久化（重启不丢失）
- 支持动态添加新文档
- 统一 JSON 返回格式
- 资料不足时明确提示无法回答

## 技术栈

- **Web 框架**：FastAPI
- **向量数据库**：ChromaDB（PersistentClient）
- **大模型**：通义千问（qwen-plus）
- **Embedding 模型**：qwen3.7-text-embedding
- **其他**：Pydantic、python-dotenv、OpenAI 兼容接口

## 项目结构