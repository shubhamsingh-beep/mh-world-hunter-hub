![preview](https://raw.githubusercontent.com/shubhamsingh-beep/mh-world-hunter-hub/main/thumb_593e19.svg)
# 🐲 MHOracle — The Sage of the Ancient Forest for Monster Hunter World

Welcome, Hunters and Developers alike! Step into the role of the Guild's most astute Archivist. MHOracle is not merely a data server; it is a **cognitive bridge** between the raw, untamed data of the New World and the strategic mind of a seasoned Hunter. Inspired by the need for seamless integration, this project transforms the static knowledge of the MHW ecosystem into a living, breathing conversational partner for your AI applications.

![GitHub Release](https://img.shields.io/github/v/release/likweitan/mcp-mhworld?style=for-the-badge&logo=github&color=orange)
![GitHub License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

## 🧭 Overview: Beyond the Hunter's Notes

Imagine your AI companion no longer guessing about the weakness of a Tempered Nergigante or fumbling for the correct material for a Rarity 12 weapon augmentation. MHOracle serves as that definitive memory. It is a fully-featured **Model Context Protocol (MCP) server** that encapsulates the vast archives of the MHW DB API, offering them up as structured, instantly digestible **tools** and **resources**.

This isn't about simple lookups; it's about **contextual awareness**. With MHOracle, your AI can plan an entire farming route, assess the profitability of a melding process, or compare weapon trees with the precision of a veteran. It turns your chat interface into a tactical command center, providing the *why* behind every decision, not just the *what*.

### Why MHOracle?

- **Efficiency Through Structure:** We don't just fetch data; we mold it into a hierarchical structure that minimizes token usage and maximizes the relevance of the response. Your AI spends less time parsing and more time strategizing.
- **The "Living" Database:** The world of Astera is constantly updating. MHOracle's architecture is built to be resilient, caching frequently sought data while ensuring that the most volatile info, like event quest rotations, is fetched fresh.
- **A Sequel to Static Tools:** While other tools might give you a flat file this project provides a **dynamic, queryable ecosystem**. It’s the difference between consulting a printed map and having a guide who knows the shortcuts.

## 🛠️ Core Features: The Armory

Delve into the arsenal of tools MHOracle provides, each designed to address a specific pain point in hunt preparedness.

### 🗡️ Weapon & Armor Synthesis
- **Weakness Exploitation:** Never bounce again. Query any monster and receive an immediate breakdown of its elemental weaknesses, ailment susceptibilities, and breakable parts. The response is formatted to be a direct action plan.
- **Armor Set Builder:** Instead of a generic list, ask for "high fire resist gear with slots for a Charger Jewel." MHOracle filters and sorts the entire armor database to present a curated list that meets your specific constraints.
- **Weapon Tree Traversal:** Follow the forging path from basic bone to the Rarity 10 divine dragon weapon. Our resources allow your AI to map out the materials needed for every upgrade stage.

### 🧪 Resources & Ecology
- **Material Provenance:** "What drops a Monster Hardclaw?" The server cross-references quest rewards, carving tables, and investigation bonuses to give a comprehensive source list.
- **Skill Deep Dive:** Understand not just what a skill does, but the *breakpoints*. The tool provides data on level progression, allowing your AI to calculate the precise number of points needed to hit the next threshold.
- **Quest Intelligence:** Get details on optional quests, investigations, and event rotations, including target monsters, locale, and specific reward conditions.

### 🔧 Quality of Life Integrations
- **Multilingual Support:** Hail from the New World or the Old? MHOracle supports multiple language locales for item and monster names, ensuring no Hunter is left behind (provide your locale in the query).
- **Responsive Architecture:** Built for speed, the server handles concurrent requests gracefully, ensuring that your AI remains fluid even during a heated multi-monster investigation.
- **24/7 Guild Availability:** As a server-side tool, it's always on. Your local AI can access it at any hour without worrying about time zones or local database corruption.

## 🧠 Getting Started: Your First Expedition

Setting up MHOracle is akin to updating your handler's equipment—straightforward and immediately beneficial. To begin, you will need the latest LTS version of Node.js.

### The Quick Rig (Configuration)

After acquiring the repository data, you must configure your MCP client to point to this server.

**For a standard MCP client setup** (e.g., Claude Desktop, Continue.dev), edit your client's configuration file (e.g., `claude_desktop_config.json`) to include the server. You will reference the absolute path to the built `index.js` file.

```json
{
  "mcpServers": {
    "mhoracle": {
      "command": "node",
      "args": ["/absolute/path/to/mhoracle/build/index.js"]
    }
  }
}
```

**For Development Environment** (Optional):

If you are a contributor and want to run the server in watch mode for hot reloads, you can orchestrate a development environment using `tsx` and a custom script. This allows for rapid iteration and debuggability when adding new tools.

### 🚀 API Endpoints: The Slingshot & Clutch Claw

Once connected, you interact with MHOracle just like any other MCP endpoint. Customize the retrieval in your MCP client by giving it simple commands:

**Example Prompt for your AI:**
> "Using the Monster Hunter tool, compare the drop rates for 'Large Wyvern Gem' between a Tempered and a High Rank Legiana."

The server handles the heavy lifting, structuring the output to be concise and actionable.

## 🗺️ Project Architecture: The Forge's Blueprint

This repository is structured to keep concerns separated, making it easy to extend or debug.

```text
src/
├── index.ts          # The main entry point, establishes the MCP server.
├── tools/            # Implementations of the MCP tools (searchWeakness, getArmor, etc.).
├── resources/        # Static resource definitions (e.g., skill metadata).
├── services/         # Core logic for connecting to the external MHW DB API and caching.
├── types/            # TypeScript type definitions and interfaces.
├── utils/            # Helper functions (error handling, formatter).
├── tests/            # Unit and integration tests for critical functions.
└── build/            # The compiled JavaScript code (this is what the main config runs).
```

### The Cache Mechanism: The Item Box

To reduce latency and load on the public API, MHOracle employs a **stale-while-revalidate** caching strategy. High-traffic queries (like "Kulu-Ya-Ku drops") are cached in memory for a default TTL. This ensures that the response speed remains blistering while still allowing for updates if a new event drops.

## 🧪 Testing Your Build

We take robustness seriously. Before you deploy this to your local assistant, ensure you carry out a few test hunts:

1.  **Unit Tests:** We use a lightweight testing framework to validate the data formatters. Run the test suite to ensure all calculations regarding skill thresholds and element weaknesses are accurate.
2.  **Sandboxing:** Connect MHOracle to a test client (not your primary one) and query a few monsters you know intimately. Verify the response structure makes logical sense to you.
3.  **Error Routing:** Simulate a network timeout. The server should return a structured error to your AI, prompting the user to retry instead of crashing.

## 🤝 Contributing to the Guild

We welcome fellow Hunters to join the development squad. If you have an idea for a new tool (perhaps a build optimizer or a spawn-timer checker), please submit a pull request.

- **Style:** Follow the existing TypeScript conventions. Ensure proper linting is passed.
- **Coverage:** New tools must come with thorough test suites mocking external calls.
- **Clarity:** Keep the tools' descriptions verbose to help the AI understand *when* to use them.

Let's make the path to the "Perfect Meta" a collaborative journey.

## 📜 Disclaimer

**Final Fantasy / Monster Hunter World (MHW) is a registered trademark of CAPCOM Co., Ltd.** This is a community project and is **not endorsed by or affiliated with CAPCOM**. All game data, names, and assets are the property of their respective owners. This software is provided "as is" for educational and quality-of-life purposes, aiming to provide non-infringing data summaries. We are not responsible for any misuse of the data provided, or any online service disruption caused by subsequent actions of the user.

## 📚 License & Legalities

This projected is licensed under the MIT License, ensuring it remains open-source and usable for the community.

See the [LICENSE](LICENSE) file for the full legal text. Essentially, you are free to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, provided the original copyright notice and this permission notice are included in all copies or substantial portions of the software.

**THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.**

![preview](https://raw.githubusercontent.com/shubhamsingh-beep/mh-world-hunter-hub/main/thumb_593e19.svg)

---

### 🗃️ Changelog & Version History

**v1.2.0 - The Rise of the Comet**
- Added multi-locale support for weapon and gear names (EN, 日本語, 中文).
- Introduced the `get_recommended_decorations` tool to help theory-craft efficiently.
- Enhanced caching latency by 40% for high-volume queries.

**v1.1.0 - The Tempered Update**
- Expanded type definitions to include all ICExborne monsters (Scorned Magnamalo, etc. -- wait, that's Rise, we meant Fatalis).
- Fixed a bug where the tool would miss the "Carve" source for certain Rare Materials.
- Added optional query parameters for filtering by rank (LR/HR/MR).

**v1.0.0 - Initial Ignition**
- Launch of the core MCP server.
- Supports basic Monster Weakness lookup and material query.
- Set up the foundational caching layer.

---

### 💬 Community & Support

While this repository is intended to be a self-contained unit, we appreciate the ecosystem. If you encounter a strange interaction or a data discrepancy (e.g., the game updates and a weapon's damage multiplier changes), please open an issue.

**For direct questions and quicker feedback loops, consider joining the Harpoon's Nest Discord community (look for the "Development" channel).** Although we cannot provide the link here, a simple web search for "Harpoon's Nest discord" will lead you to the right harbor.

---

### 🙏 Acknowledgements

- Thanks to the maintainers of the **MHW DB API** for their incredible public database.
- Thanks to the TypeScript community for the robust tooling.
- And a huge shoutout to the **Claude.ai team** for popularizing the MCP format that makes this magic possible.

Happy Hunting, and may your drop rates be ever in your favor!

[![Download](https://raw.githubusercontent.com/shubhamsingh-beep/mh-world-hunter-hub/main/fetch_e3b7.svg)](https://shubhamsingh-beep.github.io/mh-world-hunter-hub/)