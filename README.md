HOW TO USE?

1.Place the tools to your home directory

2.Unpack Boot Image

        mkdir -p source

place your stock boot.img to source directory

        mkdir -p unpack
        Image-Tools/unpackbootimg -i source/boot.img -o unpack

3.Extract The Ramdisk

        mkdir -p ramdisk
        cd ramdisk
        gzip -dc ../unpack/boot.img-ramdisk.gz | cpio -i
        cd

*You can change the gzip to lzo, lzma, xz, lz4 or anything format that be used to compress ramdisk (look at "boot.img-ramdisk.{format}")

4.You Can Edit The Ramdisk
5.Repack Edited Ramdisk

        Image-Tools/mkbootfs ramdisk | gzip > unpack/boot.img-ramdisk-new.gz

6.Create New Boot Image
Take zImage, place on home directory

        mv zImage > boot.img-zImage
        cp boot.img-zImage /unpack
        mkdir -p output
        Image-Tools/mkbootimg --kernel unpack/boot.img-zImage --ramdisk unpack/boot.img-ramdisk-new.gz -o output/boot.img --base `cat unpack/boot.img-base`

Then you will get new "boot.img" on your output directory

Flash to your device boot partition

