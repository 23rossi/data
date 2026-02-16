UBUNTU
jq -s '.[0] + (.[1] | map(select(.active == 1)))' \
  ./data/data-archive.json \
  ./data/data.json \
  | sponge ./data/data-archive.json

WINDOWS

- aktualizuje json

.\jq-win64.exe -s ".[0] + (.[1] | map(select(.active == 0)))" data-archive.json data.json > tmp.json
>> Move-Item -Force tmp.json data-archive.json

- smaz vsechny 0
.\jq-win64.exe "map(select(.active != 0))" data.json > tmp_data.json
Move-Item -Force tmp_data.json data.json

> winget install jqlang.jq
  https://github.com/jqlang/jq/releases