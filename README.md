# make 1G junk data file
dd if=/dev/zero of=data.junk bs=1M count=1024

# compress with each tool
gzip -c data.junk > data.junk.gz
tar -cf data.junk.tar data.junk
xz -zk data.junk
7za a -t7z data.junk.7z data.junk

# compress with bzip2
bzip2 -zk data.junk

# make unlimited size bzip2 archive (100TB in this case)
dd if=/dev/zero bs=10G count=10000 | bzip2 -c > not.virus.bz2

# start extracting that file
bzip2 -d not.virus.bz2
