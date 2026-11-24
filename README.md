# bruh

decrypt:
openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 -in src_code_small.tar.zst.enc -out src_code_small.tar.zst

decompress:
COPYFILE_DISABLE=1 tar -cf - ./src_code_small | zstd -T0 -19 -o src_code_small.tar.zst
