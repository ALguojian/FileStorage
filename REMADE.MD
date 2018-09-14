# android本地存储目录

- 内部存储
- 外部存储
    - 应用私有目录
    - 外部目录

## 获得内部存储目录
```
    /**
     * 获得私有目录文件，卸载之后会自动删除，7.0之后私有目录访问权限必须添加fileprovider访问
     */
    private void init() {

        //绝对路径,=/data/user/0/packname/files
        File filesDir = mContext.getFilesDir();
        filesDir.getAbsolutePath();

        //缓存路径，sp等,=/data/user/0/packname/cache
        File cacheDir = mContext.getCacheDir();
        cacheDir.getAbsolutePath();

        boolean b = mContext.deleteFile("");

        String[] strings = mContext.fileList();

        //获得私有目录内的自建目录，=/data/user/0/packname/app_myFile
        String myFile = mContext.getDir("myFile", MODE_PRIVATE).getAbsolutePath();

        //获得data目录=/data
        File dataDirectory = Environment.getDataDirectory();

    }
```

## 获得外部存储目录

```
    /**
     * 外部存储路径，sd等
     * <p>
     * /storage/emulated/0/Android/data/app package name
     */
    private void init2() {

        //在4.4以前系统中可能会获得null，因为4.4之前如果没有插sd卡，就代表没有外部存储，
        //获得某个应用在外部存储中的files路径，=/storage/emulated/0/Android/data/packname/files
        File externalFilesDir = mContext.getExternalFilesDir("");
        String absolutePath = externalFilesDir.getAbsolutePath();

        //获得某个应用在外部存储中的cache路径,=/storage/emulated/0/Android/data/packname/cache
        String absolutePath1 = mContext.getExternalCacheDir().getAbsolutePath();


        //通过Environment获得的时候需要申请权限,获得外部存储的根路径=/storage/emulated/0
        String absolutePath3 = Environment.getExternalStorageDirectory().getAbsolutePath();

        //,获得外部存储的根路径=/storage/emulated/0
        String absolutePath2 = Environment.getExternalStoragePublicDirectory("").getAbsolutePath();

    }

```

# 获得外部存储目录

```
 /**
     * 获得外部存储路径,包括机身外部存储以及sd卡存储
     */
    public void getExternalStoragePath() {

        File[] files;
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.KITKAT) {
            files = mContext.getExternalFilesDirs(Environment.MEDIA_MOUNTED);
            for (File file : files) {
                Log.e("main", file.getPath());
            }
        }
    }
```

# 其他目录
```
     Environment.getDownloadCacheDirectory();//,=/cache
     Environment.getRootDirectory();//,=system
```