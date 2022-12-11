# Discord-torrent

# Example usage
```js
const Discord = require("discord.js");
const { EmbedBuilder, ActionRowBuilder, ButtonBuilder } = require('discord.js');

const torrent_module = require('discord-torrent')
const torrent = require('discord-torrent')

module.exports = {
    name: "torrent",
    aliases: ['1337x'],
    description: "search torrent",
    usage: ".torrent <torrent name>",
    run: async (client, message, args) => {
    if(!args.length) {
        return message.channel.send("What do you want to download?")
          }


      message.channel.send({ content: "`Searching...`" })
      let query = "";
      args.map(string=> {
          query += " " + string;
      });
      torrent_module.grabTorrents(query)
      .then(torrentArray => {

          if (torrentArray.length > 0)
          {

              const torrentList = new EmbedBuilder()
              torrentArray.map((torrent) => {
                torrentList.addFields(
                    { name : `${torrent.number}. ${torrent.title}`, value : `${torrent.magnet} | Seeders: ${torrent.seeds} | Size: ${torrent.size} | Time: ${torrent.time}`}
                )
            });
            message.reply({ embeds: [torrentList] }); //Send them the list of torrents in the channel


          }
          else
          {
              
            const error = new EmbedBuilder()
            .setTitle("Not found")
            .addFields({ name: 'Message', value: 'Torrent not found!.', inline: true })
            .setTimestamp()
            message.reply({ embeds: [error] });
              
          }

      });
   
  }}
  ```
![enter image description here](https://cdn.discordapp.com/attachments/718452489342550037/1051576294573359215/Screenshot_from_2022-12-11_20-08-29.png)

