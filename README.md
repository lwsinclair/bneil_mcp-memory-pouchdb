[![MseeP.ai Security Assessment Badge](https://mseep.net/pr/mcp-mirror-bneil-mcp-memory-pouchdb-badge.png)](https://mseep.ai/app/mcp-mirror-bneil-mcp-memory-pouchdb)

# Memory Custom : PouchDB 🧠

[![smithery badge](https://smithery.ai/badge/@bneil/mcp-memory-pouchdb)](https://smithery.ai/server/@bneil/mcp-memory-pouchdb)

This project adds new features to the Memory server offered by the MCP team. It allows for the creation and management of a knowledge graph that captures interactions via a language model (LLM). 🚀

This repo was forked from [https://github.com/BRO3886/mcp-memory-custom](https://github.com/BRO3886/mcp-memory-custom) which was a great starting point, thanks again for fixing timestamps. This repo's goal was more to fix the issue with an ever increasing json file for context.

## New Features ✨

### 1. PouchDB Integration 💾

- The server now uses PouchDB for robust document-based storage
- **Why?**: Better data consistency, built-in versioning, and improved performance for large datasets
- Maintains file backup for compatibility

### 2. Custom Memory Paths 📁

- Users can now specify different memory file paths for various projects
- **Why?**: This feature enhances organization and management of memory data, allowing for project-specific memory storage

### 3. Timestamping ⏰

- The server now generates timestamps for interactions
- **Why?**: Timestamps enable tracking of when each memory was created or modified, providing better context and history for the stored data

## Getting Started 🚀

### Prerequisites 🔧

- Node.js (version 16 or higher)
- PouchDB (automatically installed as a dependency)

### Installing via Smithery 📦

To install Knowledge Graph Memory Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@bneil/mcp-memory-pouchdb):

```bash
npx -y @smithery/cli install @bneil/mcp-memory-pouchdb --client claude
```

### Installation 🛠️

1. Clone the repository:

   ```bash
   git clone git@github.com:bneil/mcp-memory-pouchdb.git
   cd mcp-memory-pouchdb
   ```

2. Install the dependencies:

   ```bash
   npm install
   ```

### Configuration ⚙️

The server requires two environment variables to be set:

1. `MEMORY_FILE_PATH`: The absolute path where the memory backup file will be stored
2. `POUCHDB_PATH`: The absolute path where the PouchDB database will be stored

Example configuration in your `claude_desktop_config.json` / `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "memory": {
      "command": "node",
      "args": ["/path/to/mcp-memory-pouchdb/dist/index.js"],
      "env": {
        "MEMORY_FILE_PATH": "/path/to/custom/memory.json",
        "POUCHDB_PATH": "/path/to/custom/pouchdb_directory"
      }
    }
  }
}
```

The server will fail to start if either environment variable is not set. 🚫

Optional environment variables:
- `POUCHDB_OPTIONS`: JSON string of additional PouchDB configuration options

### Running the Server 🚀

#### Updating the mcp server json file 📝

Add this to your `claude_desktop_config.json` / `.cursor/mcp.json` file:

```json
{
  "mcpServers": {
    "memory": {
      "command": "node",
      "args": ["/path/to/mcp-memory-pouchdb/dist/index.js"],
      "env" : {
        "MEMORY_FILE_PATH":"/home/.../local_dbs/memory.json",
        "POUCHDB_PATH":"/home/.../local_dbs/pouchdb"
      }
    }
  }
}
```

System Prompt changes:

```
Follow these steps for each interaction:
1. User Identification:
   - You should assume that you are interacting with default_user
   - If you have not identified default_user, proactively try to do so.

2. Memory Retrieval:
   - Always begin your chat by saying only "Remembering..." and retrieve all relevant information from your knowledge graph
   - Always refer to your knowledge graph as your "memory"

3. Memory
   - While conversing with the user, be attentive to any new information that falls into these categories:
     a) Basic Identity (age, gender, location, job title, education level, etc.)
     b) Behaviors (interests, habits, etc.)
     c) Preferences (communication style, preferred language, etc.)
     d) Goals (goals, targets, aspirations, etc.)
     e) Relationships (personal and professional relationships up to 3 degrees of separation)

4. Memory Update:
   - If any new information was gathered during the interaction, update your memory as follows:
     a) Create entities for recurring organizations, people, and significant events, add timestamps to wherever required. You can get current timestamp via get_current_time
     b) Connect them to the current entities using relations
     c) Store facts about them as observations, add timestamps to observations via get_current_time


IMPORTANT: Provide a helpful and engaging response, asking relevant questions to encourage user engagement. Update the memory during the interaction, if required, based on the new information gathered (point 3).
```

#### Running the Server Locally 💻

To start the Knowledge Graph Memory Server, run:

```bash
npm run build
node dist/index.js
```

The server will listen for requests via standard input/output.

## API Endpoints 🔌

The server exposes several tools that can be called with specific parameters:

- **Get Current Time** ⏰
- **Set Memory File Path** 📁
- **Create Entities** ➕
- **Create Relations** 🔗
- **Add Observations** 📝
- **Delete Entities** ❌
- **Delete Observations** 🗑️
- **Delete Relations** 🔗
- **Read Graph** 📖
- **Search Nodes** 🔍
- **Open Nodes** 🔓

## Acknowledgments 🙏

- Inspired by the Memory server from Anthropic
- Powered by PouchDB for robust data storage 💾
