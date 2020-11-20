1. Upload scripts
   1. rclone_mount(Disable Docker Starts for now) -> Cron Job Every 10 minutes
   2. rclone_upload -> Cron Job 3 AM PST
   3. rclone_unmount -> Array stop
2. Update PlexLibrary settings to disable "Empty Trash automatically after every scan"
   1. https://support.plex.tv/articles/201154537-move-media-content-to-a-new-location/
3. Disable remote access
4. Spin down impacted Dockers:
   1. plex
   2. sonarr
   3. radarr
   4. nzbget
   5. ombi
5. Unmount current rClone mounts
6. Disable existing scripts
7. Disable AutoStart on impacted Dockers:
   1. plex
   2. sonarr
   3. radarr
   4. nzbget
   5. ombi
8. Restart Unraid for a clean slate
9. Run mount script manually
10. Verify mounts are created
   1. /mnt/user/gDrive   # Should be the Google Drive online mount
   2. /mnt/user/gDriveStaging # Should be the local staging area, should have empty folders created
   3. /mnt/user/mergerFS  # Should be the merged files directory.
      1. Create file in /mnt/user/mergerFS/tmpFolder/, it should appear in the /mnt/user/gDriveStaging/tmpFolder
      2. Mount /mnt/user/mergerFS to filebot, scan a TV season and verify episode details are readable and that VFS cache is used
         1. check /mnt/user/rCloneCache/gdrive_secure/vfs
11. Stop Array and verify mounts are removed
    1. /mnt/user/gDrive   # Should be empty
    2. /mnt/user/gDriveStaging # Should have tmpfile in it
    3. /mnt/user/mergerFS  # Should be empty
12. Start Array and verify mounts are created properly
    1. /mnt/user/gDrive   # Should be the Google Drive online mount
    2. /mnt/user/gDriveStaging # Should be the local staging area, should have empty folders created
    3. /mnt/user/mergerFS  # Should be the merged files directory.
       1. Create file in /mnt/user/mergerFS/tmpFolder/, it should appear in the /mnt/user/gDriveStaging/tmpFolder
       2. Mount /mnt/user/mergerFS to filebot, scan a TV season and verify episode details are readable and that VFS cache is used
       3. check /mnt/user/rCloneCache/gdrive_secure/vfs
13. Update Plex Mappings
    1. /tv -> /mnt/user/mergerFS/NewBBB/TV
    2. /user -> /mnt/user/
14. Add TV Path to Library
    1. /user/mergerFS/NewBBB/TV
15. Scan should start, if not trigger by doing a "Scan Library Files"
16. Verify everything has two items - CURRENT STEP
17. Remove existing /TV mapping from Library
18. After scan verify that there are deleted items and then empty trash
    1. https://support.plex.tv/articles/200289326-emptying-library-trash/
19. Re-enable "Empty Trash automatically after every scan"
    1.  https://support.plex.tv/articles/201154537-move-media-content-to-a-new-location/
20. Remove old /TV mapping from Plex Docker
21. Perform same steps for Movies
22. Update Sonarr with following mounts
    1. /user --> /mnt/user
    2. Remove /TV and /Downloads
23. Add new root folder
    1. https://tv.sonnarSite.io/settings/mediamanagement
    2. /user/mergerFS/NewBBB/TV
24. Change root path on TV Shows
    1. https://tv.sonarrSite.io/serieseditor
    2. Create filter for root folder
    3. Update root folder
25. Verify TV shows appear properly and file scans work
26. Update Radarr with following mounts
    1. /user --> /mnt/user
    2. Remove NewBBB and Downloads
27. Add new root folder
    1. https://movies.radarrSite.io/settings/mediamanagement
    2. /user/mergerFS/NewBBB/Movies
28. Change root path on Movies
    1. https://movies.radarrSite.io
    2. Movie Editor
    3. Custom Filter
    4. Update Root Folder
29. Verify Movies appear properly and file scans work
30. Update NZBGet Mounts
    1.  /user --> /mnt/user
    2.  Keep /mnt/user/Downloads
31. Update NZBGet Paths
    1.  MainDir --> /mnt/user/mergerFS/downloads
32. Test downloading a TV show and movie
33. Verify it copies into /NewBBB properly
34. Verify it is stored on /mnt/user/gDriveStaging/NewBBB/*
35. Run Upload script 30 minutes later