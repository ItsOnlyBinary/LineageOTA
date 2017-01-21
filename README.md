# LineageOTA
A simple OTA REST Server for LineageOS OTA Updater System Application

## How to use
1. `cd /var/www/ && composer create-project julianxhokaxhiu/lineage-ota LineageOTA`
3. Follow the rest of the tutorial on [my personal blog post](http://blog.julianxhokaxhiu.com/entry/how-the-cm-ota-server-works-and-how-to-implement-and-use-ours) where I explain how to override the build server on your ROM.
4. Optional. If just want to test if the REST Server is working, if you go to [http://localhost/LineageOTA](http://localhost/LineageOTA/) you'll be redirected to the builds directory listing.

or

```
docker run \
    --restart=always \
    -d \
    -p 80:80 \
    -v "/home/user/builds:/var/www/html/builds/full" \
    julianxhokaxhiu/lineageota
```

## Where do I have to upload the ZIPs that I obtain after the compilation?
- Full builds should be uploaded to `builds/full` directory.
- Delta builds will be automatically built on the `builds/delta` directory.

## Can I Debug my REST Server somehow?
Yes, you can! I've implemented a [simple script](https://github.com/julianxhokaxhiu/LineageOTAUnitTest) made for NodeJS that you clone and use it.

## Changelog
### v2.0.9
- Removing XDelta3 logic for Delta creation ( see https://forum.xda-developers.com/showthread.php?p=69760632#post69760632 for a described correct process )
- Prevent crash of the OTA system if a file is being accessed meanwhile it is being uploaded

### v2.0.8
- Adding support for LineageOS CMUpdater ( this should not break current CM ROMs support, if yes please create an issue! )

### v2.0.7
- Renamed the whole project from CyanogenMod to LineageOS
- Added support for LineageOS ( and kept support for current CyanogenMod ROMs, until they will transition to LineageOS)

### v2.0.6
- Loop only between .ZIP files! Before even .TXT files were "parsed" which wasted some memory. Avoid this and make the REST server memory friendly :)
- HTML Changelogs! If you will now create a changelog file next to your ZIP file with an HTML extension ( eg. `lineage-14.0-20161230-NIGHTLY-hammerhead.html` ) this will be preferred over .TXT ones! Otherwise fallback to the classic TXT extension ( eg. `lineage-14.0-20161230-NIGHTLY-hammerhead.txt` )

### v2.0.5
- Fix the parsing of SNAPSHOT builds

### v2.0.4
- Final Fix for TXT and ZIP files in the same directory
- Automatic URL detection for basePath ( no real need to touch it again )
- Delta builds array is now returned correctly

### v2.0.3
- Memcached support
- UNOFFICIAL builds support ( they will be set as channel = NIGHTLY )
- Fix Delta Builds path
- Fix internal crash when *.txt files were present inside /builds/full path

### v2.0.2
- Fix some breaking changes that will not enable the REST server to work correctly.

### v2.0.1
- Excluded hiddens files and autogenerated ones by the OS (for example `.something` or `Thumbs.db`).

### v2.0
- Refactored the whole code.
- Now everything is PSR4 compliant.
- Introduced composer.json to make easier the installation of the project.

## Drawbacks
- Delta updates may or may not work. It's using Deltax3 to create them but it's just experimental. Use it at your own risk.


## License
See [LICENSE](https://github.com/julianxhokaxhiu/LineageOTA/blob/2.0/LICENSE).

Enjoy :)