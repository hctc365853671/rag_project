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
Day19_rag_project/
├── chroma_db/              # 向量数据库持久化目录（自动生成）
├── .env                    # 环境变量（存放 API Key）
├── main.py                 # FastAPI 入口文件
├── rag.py                  # 知识库构建、检索、追加逻辑
├── llm.py                  # 大模型调用与回答生成
├── models.py               # Embedding 向量化
├── chatRequest.py          # 请求数据模型
└── README.md
└── requirements.txt        #安装依赖

## 安装与运行

### 1. 进入项目目录

```bash
cd Day19_rag_project

2. 创建虚拟环境并安装依赖
python -m venv venv

# Windows Git Bash
source venv/Scripts/activate

# 安装依赖
pip install -r requirements.txt

3. 配置环境变量
在项目根目录创建 .env 文件，内容如下：
QWEN_KEY=你的通义千问API_Key
4. 启动服务
uvicorn main:app --reload
启动成功后可访问：
接口文档：http://127.0.0.1:8000/docs
服务地址：http://127.0.0.1:8000
接口说明
1. 智能问答
接口：POST /chat
请求体：{
  "content": "这个投影仪重量是多少？"
}
返回示例{
  "code": 200,
  "message": "success",
  "data": "根据产品资料，该投影仪重量约480克。"
}

无相关资料时{
  "code": 200,
  "message": "success",
  "data": "根据现有资料无法回答"
}

添加文档
接口：POST /add_document
请求体：{
  "content": "这里是要新增的产品说明内容..."
}
返回示例{
  "code": 200,
  "message": "存入成功"
}

核心流程说明
启动时：自动构建知识库并写入 ChromaDB（如果已有数据则跳过）
用户提问：将问题转为向量，在知识库中检索最相关的内容
生成回答：把检索到的内容作为参考资料，交给通义千问生成最终回答
添加文档：对新内容进行切分和向量化，追加到现有知识库中
注意事项
.env 文件不要上传到 GitHub
chroma_db 文件夹是向量数据库的本地存储，可保留
首次启动会进行向量化，需要一些时间
添加文档后立即生效，可直接提问新内容
后续可优化方向
支持 PDF / Word 文件上传解析
增加多轮对话记忆
添加简单前端界面（Streamlit / Gradio）
接口鉴权与限流
优化文档切分策略，提升检索准确率
作者
个人 AI 应用学习项目。
