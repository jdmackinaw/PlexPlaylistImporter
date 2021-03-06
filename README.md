Plex Playlist Importer - v1.0.0.x http://www.castledragmire.com/Projects/Plex_Playlist_Importer

# Import playlists into Plex

My music directories have been growing for over 2 decades in a folder based hierarchy, often using playlists for organization. Plex’s music organization is counterintuitive to this organizational structure, and Plex currently does not have an easy way to import external playlists. Hence this script was born :-)

While this script requires Python 3 (compiled against v3.4), a stand-alone Windows binary version is also available on the URL at the top of this file.<br>
If running through the Python source, The Python sqlite3 lib is required, but it should come with Python.

##Parameters:
1. (Required): The path of the playlist file. If the file extension is not recognized, the file is parsed as a Winamp playlist (.m3u)
2. (Required): The name of the playlist in Plex to import to. If it does not exist, the program will prompt on whether to create it
3. (Optional): The path to the sqlite3 database file
  * The program tries to guess the path for the Plex data directory. If it cannot be found, this path needs to be passed explicitly
  * If the database is still not found from the given Plex path, the full path to the database is required
    * If this is required, try searching in the Plex directory for “com.plexapp.plugins.library.db” (or *.db) and passing the result’s file path directly as the parameter

The only playlist type that is currently supported is Winamp playlists (.m3u).<br>
Playlist importers just collect the absolute files names, and others can easily be dropped into the “Importers” directory without any other code changes.<br>
While the M3U importer (Importers/M3U.py) is the most appropriate to use as a template, I included a second example one (PTL.py) which just pulls in absolute file names with no error checks.

PlexPlaylistImporter.sh is just included to force proper Unicode (utf-8) encoding on the console.

##How it works
The songs you want to play have to already exist in the Plex database.<br>
When you add a song to Plex (through Plex), it stores the song’s full file path in the Plex database. What this script does is derive all the full song paths in a playlist file that you give it, checks those paths against Plex’s database, and then adds the matches in the proper order into the Plex playlist you specified.<br>
So for this reason, the script must be ran on the same computer running the Plex server so that it can match the paths.

Copyright and coded by Dakusan - See http://www.castledragmire.com/Copyright for more information.