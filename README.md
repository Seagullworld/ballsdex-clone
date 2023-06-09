@@ -13,7 +13,7 @@ BallsDex is a bot for collecting countryballs on Discord and exchange them with

You can invite the bot [here](https://discord.com/api/oauth2/authorize?client_id=999736048596816014&permissions=537193536&scope=bot%20applications.commands).

[![Discord server](https://discordapp.com/api/guilds/1049118743101452329/embed.png?style=banner3)](https://discord.gg/Qn2Rkdkxwc)
[![Discord server](https://discordapp.com/api/guilds/1049118743101452329/embed.png?style=banner3)](https://discord.gg/Qn2Rkdkxwc) [![Self-host server](https://discordapp.com/api/guilds/1078701108500897923/embed.png?style=banner3)](https://discord.gg/M4gVaRrRDe)

## Suggestions, questions and bug reports

@@ -23,98 +23,11 @@ we'll do it for you).

You can directly post an issue in this repo, be sure to use the template!

## Running the bot
## Documentation

The bot comes as a [poetry](https://python-poetry.org/) Python package and can run using Docker.

You must first setup a Discord bot. **The privileged message content intent is required!**

### With Docker (recommended)

1. Install Docker on your machine. We assume you have the correct permissions to run commands.
2. At the root of the repository, run `docker compose build`
3. Add a text file `.env` at the root of the repository in the following form:

   ```env
   BALLSDEXBOT_TOKEN=your token here
   POSTGRES_PASSWORD=a random string
   ```

   If you want to override the default prefix for text commands (`b.`), add this line

   ```env
   BALLSDEXBOT_PREFIX=custom_prefix
   ```

4. Run the bot with `docker compose up -d`

The bot will be running in detached mode. You can view the logs with `docker compose logs -f`.

If you want to shutdown the bot, run `docker compose down`.

When updating the bot, do the following:

1. `git pull`
2. `docker compose build`
3. `docker compose down && docker compose up -d`

### Without Docker

**This part is not supported.** I use docker myself for production, and run the `db` and
`redis-cache` services from `docker-compose` for development.

We assume that you have Python 3.10 and pip installed.

1. Start a PostgreSQL server on the host.
   1. Create a postgres user and database.
2. Start a Redis serve on the host.
3. Install poetry with `pip install poetry`.
4. Run `poetry install`
5. Export the following environment variables:

   - `BALLSDEXBOT_TOKEN`: the Discord bot token
   - `BALLSDEXBOT_DB_URL`: a link in the form `postgres://{postgres user name}:{postgres password}@localhost:5432/{database name}`
   - `BALLSDEXBOT_REDIS_URL`: a link in the form `redis://localhost`

   Replace `localhost` with any host when appropriate.

6. Run `poetry run python3 -m ballsdex`

There are some command line options available when starting the bot.
See them with `python3 -m ballsdex --help`.

## Using the admin panel

Go to https://localhost:8000/admin/init to create the first admin user (you).

You now have access to the admin panel for adding new balls, and managing everything!

If you encounter a 403 error, click the logout button in the top right corner, and login again.

**Unless you know about networking and security, it is not recommended to expose this website.**

## Configuring admin commands

There is a `/admin` command available for providing useful tools for the bot admins (anti cheat,
giving items, forcing spawn and blacklist management).

It has to be enabled explicitely by adding the following lines in your `.env` file:

```env
BALLSDEXBOT_ADMIN_GUILDS=ID1,ID2,...
BALLSDEXBOT_ADMIN_ROLES=ID1,ID2,...
BALLSDEXBOT_ROOT_ROLES=ID1,ID2,...
```

- `BALLSDEXBOT_ADMIN_GUILDS` is for the servers where you want to register the admin slash command.
  That way, it will not be visible to other servers.
- `BALLSDEXBOT_ADMIN_ROLES` allows the given roles to use `/admin guilds` and `/admin blacklist`.
  These are your moderators that help for anti cheat.
- `BALLSDEXBOT_ROOT_ROLES` allows the given roles to use `/admin spawn` and `/admin give`, in
  addition to the commands above. Be careful who you grant this permission to!

You can have multiple servers with admin commands, but having the roles configured alongside is a
strict requirement, even for the owners.
You can learn how to setup Ballsdex and use all of its tools on the
[wiki](https://github.com/laggron42/BallsDex-Discordbot/wiki/)!
More sections are added progressively.

## Supporting

