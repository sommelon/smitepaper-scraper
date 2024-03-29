# Project archived
Starting from patch 10.4, they changed the site structure and started uploading the wallpapers on Google Drive.
Only the vertical cards can be scraped, but they aren't even the full size.
This program should still work, but only on the older patch notes.
There is no need to use it for scraping though, since all the data is in the `data` directory.


# Smitepaper
## Smite wallpaper scraper

#### DISCLAIMER
This project is for education purposes only, I am not responsible for what someone decides to do with it.

## Usage

### Download wallpapers from scraped links
```
usage: smitepaper.py download [-h] [--log] [-s SLUGS [SLUGS ...] | -i SLUGS]
                              [-g GODS [GODS ...]] [--skins SKINS [SKINS ...]]
                              [--sizes SIZES [SIZES ...]]
                              [--input-file INPUT_FILE]
                              [--output_filepath OUTPUT_FILEPATH]
```

## No need to use these
### Scrape slugs and links to wallpapers
```
usage: smitepaper.py scrape [-h] [--log] [-s SLUGS [SLUGS ...] | -i SLUGS]
                            [-g GODS [GODS ...]] [--skins SKINS [SKINS ...]]
                            [--sizes SIZES [SIZES ...]]
                            [--output-format {god,skin,link,size,slug} [{god,skin,link,size,slug} ...]]
                            [--limit LIMIT] [--offset OFFSET]
                            [--sof SLUGS_OUTPUT_FILE]
                            [--slugs-filemode {l,o,u}]
                            [--wallpapers-filemode {o,u}]
                            [--wof WALLPAPERS_OUTPUT_FILE]
                            {slugs} ...

subcommands:
  {slugs}
    slugs               scrape slugs only
```

### Scrape slugs only
```
usage: smitepaper.py scrape slugs [-h] [--limit LIMIT] [--offset OFFSET]
                                  [--sof SLUGS_OUTPUT_FILE]
                                  [--slugs-filemode {l,o,u}]
```

### Process
- Grab all the slugs of posts with the tag `Update Notes` on the [https://www.smitegame.com/news/](https://www.smitegame.com/news/) page.
- The slugs are saved to `slugs.csv` by default and the second time the script is run and the file exists, the slugs are read from there.
- Iterate through each slug, visit every post and write the god name, skin name, link to the image, the image size and the slug to `wallpapers.csv` if it's not there already by default (see `filemode` options).
- Note that some skins don't have links to images, but they are still written to the csv file.
- The files are kept in this repo, so there is no need to repeat the process, unless they are out of date.
- `gods.txt` contains the names of the gods. Those are not scraped so it needs manual updates. They are needed to guess the god name from skin name.
- To keep the csv file up to date, only specify the slugs from which to grab the new wallpapers. It will be significantly faster.
- There shouldn't be any duplicates if you run the script twice in a row with the same arguments. If there are, let me know by creating an issue.

### TODOs
- [x] Extract the god name from the skin name to allow for better file naming
- [x] Download wallpapers from the scraped links
- [x] Add progress bar ([tqdm](https://github.com/tqdm/tqdm))
- [ ] Add command line arguments to:
    - [x] Specify file names from/to which to read/write
    - [x] Specify file name format for the wallpapers
    - [ ] Decide whether to scrape skins that don't have wallpapers
    - [x] Switch between scraping and downloading
    - [ ] Specify date range of the patch notes
