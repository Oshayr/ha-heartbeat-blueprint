# ha-heartbeat-blueprint
[![View on GitHub](https://img.shields.io/badge/GitHub-View%20Repository-blue?logo=github)](https://github.com/Oshayr/ha-heartbeat-blueprint)
[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2FOshayr%2Fha-heartbeat-blueprint%2Frefs%2Fheads%2Fmain%2Fautomation%2Fheartbeat.yaml)

## Home Assistant automation blueprint: periodic Home Devices heartbeat with LLM summary

Generates an automatic, token-aware summary of everything that changed in your
smart-home during a configurable look-back window (1 h – 24 h), then posts the
result as a persistent notification—or hands it to your favourite LLM
(OpenAI, Anthropic, local Llama 2…) for a human-friendly digest.

| Blueprint UID | Version | HA min ver. | License |
|---------------|---------|-------------|---------|
| `oshayr/heartbeat` | 1.0.0 | 2024.6.0 | MIT |

## Features
* Conveys a periodic pulse of “what’s up right now”
* **Time-window reports** – 30 min → Daily
* **Token-aware** prompt shortening
* **Area / domain / state filters**
* **Raw or summary output modes**
* **Works with any Conversation agent**
* Generates a professional summary of smart-home *activity* during the last **X hours** (default 24 h;).
* Sends the result as a persistent notification.

## Installation

1. Copy the raw URL: https://raw.githubusercontent.com/Oshayr/ha-heartbeat-blueprint/refs/heads/main/automation/heartbeat.yaml

2. In Home Assistant → *Settings › Automations & Scenes › Blueprints › Import Blueprint* → paste the URL.

3. Create a new automation from the imported blueprint, adjust the settings, and you’re done.

## Inputs explained
| Title | Description | Default |
|---------------|----------------------|---------|
| Run every | How often the report should run (30min, 1 hour, 3 hours, 6 hours, 12 hours, 24 hours) | 24 hours |
| Look-back period (h) | How many hours of activity to summarise (1 – 24) | 24 |
| Conversation agent | Pick the Conversation / LLM agent that should receive the prompt | chatgpt |
| Max prompt length (chars) | Absolute ceiling for the size of the text sent to the LLM. 1 token ≈ 4 chars, so 4 096 chars ≈ 1 024 tokens | 4096 |

### Advanced settings
| Title | Description | Default |
|---------------|----------------------|---------|
| extra_prompt | Extra LLM instructions | empty |
| Output mode | summary → run the LLM and show its summary, raw → skip the LLM call and show the activity list verbatim | summary |
| Message ID | The message Id for the LLM chat and the notificatins | HeartBeat |
| Skip notification | Skip notification when nothing changed | false |

### Filters
| Title | Description | Default |
|---------------|----------------------|---------|
| Domains to ignore | List of Domains to be ignored | 'sensor', 'automation', 'script', 'camera' |
| States to ignore | List of States to be ignored | 'unavailable', 'unknown', '' |
| Areas to ignore | List of Areas to be ignored | Empty |
| Entities to ignore | List of Entities to be ignored | Empty |
  
## Changelog
* **1.0.0** – initial public release

## ToDo
* Notification choice
* Home Assistant system data + prompt

## Contributing

Contributions are welcome! Please follow these steps to contribute:

1. Fork the repository.
2. Create a new branch (\`git checkout -b feature/your-feature-name\`).
3. Make your changes and commit them (\`git commit -am 'Add new feature'\`).
4. Push to the branch (\`git push origin feature/your-feature-name\`).
5. Create a new Pull Request.

For major changes, please open an issue first to discuss what you would like to change.

## License
MIT © 2025 Oshayr
