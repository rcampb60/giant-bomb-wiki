# The Giant Bomb Wiki

A wiki about videogames.

## Getting Started

### Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop) installed and running.

### Running the Wiki for the First Time

1. Clone the repository and navigate to the root directory.
2. Start the containers:
   ```bash
   docker compose up -d
   ```
3. Open your browser and visit [http://localhost:8080](http://localhost:8080). The MediaWiki installer will launch.
4. Follow the prompts until you reach the **"MediaWiki 1.43.1 installation"** page.
5. Use the values from `docker-compose.yml` for the database connection:
   - Host: `db`
   - Other fields as specified in the file
6. Continue through the installer:
   - Name your wiki and set up an administrator username/password.
   - Select **"Ask me more questions."** to reveal additional options:
     - Choose **"Authorized editors only"**
     - Select **"Creative Commons Attribution-NonCommercial-ShareAlike"**
     - Disable outbound email
     - Choose a default skin
     - Enable all extensions
     - Enable file uploads
7. At the end of the install process, a `LocalSettings.php` file will be downloaded. Move this file into the `/config` folder.
8. Restart the containers:
   ```bash
   docker compose restart
   ```
9. Wait ~10 seconds for the database to finish patching (you can monitor via container logs).
10. Your wiki is now live at [http://localhost:8080](http://localhost:8080).

### Verifying Installation

Visit [http://localhost:8080/index.php/Special:Version](http://localhost:8080/index.php/Special:Version) to confirm everything is loaded:

#### Skins

- GiantBomb
- Vector

#### Extensions

- Semantic Extra Special Properties
- Semantic MediaWiki
- Semantic Result Formats
- Semantic Scribunto
- CodeEditor
- WikiEditor
- Scribunto
- TemplateData
- TemplateStyles
- TemplateStylesExtender

### Semantic MediaWiki Example

To test Semantic annotations, create a page (e.g. `The Legend of Zelda: Twilight Princess`) with:

```wiki
{{#set:
Has Name=Pitfall
|Has Platform=Xbox
|Has Platform=Playstation
|Has Platform=iPhone
|Has Release=Aug 09, 2012
}}
```

Then create a `Games` page with:

```wiki
{{#ask:
[[Has Platform::Xbox]]
|mainlabel=Game
|?Has Release=Release Date
}}
```

## Contributing

Interested in helping to develop the wiki? See [`CONTRIBUTING.md`](./CONTRIBUTING.md) for development and coding standards.
