# Services


## Setup

1. Create a `DataVol` directory on your home
2. Mount whatever volume/storage/disk you have on `/home/${USER}/DataVol`
3. Run `init_folders.sh` or create the folders as done there. **Folder structure is fundamental to make the whole system work**
4. Run the services with `UID=1000 GID=1000 docker compose -f /path/to/service/composefile.yml up -d`

> Remember to set and pass GID and UID, otherwise the containers will write files as root and a lot of things will break.

## Rationale for the folder hierarchy

To take advantage of hardlinks and avoid copying the same file twice, it's necessary to organize and mount folders inside the containers in a very specific way.

[As better explained in TRaSH Guides](https://trash-guides.info/File-and-Folder-Structure/How-to-set-up/Native/), the folder structure should be something like this:

```
data/
    media/
        tvshows/
        movies/
        music/
    torrents/
        downloads/
        tvshows/
        movies/
        music/
```

and mount them in a way that containers can work on the same path and thus create hardlinks.

## TODOs
- [ ] automate GID and UID variables set 

