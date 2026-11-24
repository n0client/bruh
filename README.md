# bruh

compress/encrypt/split:
COPYFILE_DISABLE=1 tar -cf - ./src_code_small \
  | zstd -T0 -19 \
  | openssl enc -aes-256-cbc -salt -pbkdf2 -iter 600000 -out src_code_small.tar.zst.enc &&
split -n 2 src_code_small.tar.zst.enc src_code_small.tar.zst.enc.part_

join/decrypt/extract:
cat src_code_small.tar.zst.enc.part_* \
  | openssl enc -d -aes-256-cbc -pbkdf2 -iter 600000 \
  | unzstd \
  | tar -xf -
