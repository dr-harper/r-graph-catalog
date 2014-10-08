

```r
# Copy files over to r-graph-catalog app

## get top-level directory for this project
proj_dir <-
  normalizePath(if(basename(getwd()) == "scripts") ".." else getwd())


# create thumbnails directory if does not exist
out_thumb_dir <- file.path(proj_dir, "r-graph-catalog", "www", "thumbnails")
if(!file.exists(out_thumb_dir)) {
  dir.create(out_thumb_dir)
}

# create figures directory if does not exist
out_fig_dir <- file.path(proj_dir, "r-graph-catalog", "www", "figures")
if(!file.exists(out_fig_dir)) {
  dir.create(out_fig_dir)
}


# get R files
r_files <-
  list.files(file.path(proj_dir, "figures"), pattern = ".R", recursive = TRUE)

# get thumbnail files
thumbs <-
  list.files(file.path(proj_dir, "figures"), pattern = "_thumb.png",
             recursive = TRUE)

# get image files
all_imgs <-
  list.files(file.path(proj_dir, "figures"), pattern = ".png", recursive = TRUE)

# remove thumbnails
figures <- all_imgs[grep("_thumb", all_imgs, invert = TRUE)]


# copy files from figures dir into app dir
r_files_copied <-
  file.copy(file.path(proj_dir, "figures", r_files),
            file.path(proj_dir, "r-graph-catalog", "data"), overwrite = TRUE)

if(all(r_files_copied)) {
  message(paste(length(r_files),
                "*.R files successfully copied into r-graph-catalog/data"))
} else {
  failed <- rfiles[which(r_files_copied == FALSE)]
  message(paste("Failed to copy the following files:", failed))
}
```

```
## 123 *.R files successfully copied into r-graph-catalog/data
```

```r
thumbs_copied <-
  file.copy(file.path(proj_dir, "figures", thumbs), out_thumb_dir, 
            overwrite = TRUE)

if(all(thumbs_copied)) {
  message(paste(length(thumbs),
                "*_thumb.pngs successfully copied into r-graph-catalog/www/thumbnails"))
} else {
  failed <- thumbs[which(thumbs_copied == FALSE)]
  message(paste("Failed to copy the following files:", failed))
}
```

```
## 123 *_thumb.pngs successfully copied into r-graph-catalog/www/thumbnails
```

```r
figs_copied <-
  file.copy(file.path(proj_dir, "figures", figures), out_fig_dir,
            overwrite = TRUE)

if(all(figs_copied)) {
  message(paste(length(figures),
                "*.pngs successfully copied into r-graph-catalog/www/figures"))
} else {
  failed <- figures[which(figs_copied == FALSE)]
  message(paste("Failed to copy the following files:", failed))
}
```

```
## 123 *.pngs successfully copied into r-graph-catalog/www/figures
```


---
title: "04_copy-files-into-r-graph-catalog.R"
author: "jzhao"
date: "Wed Oct  8 16:25:34 2014"
---