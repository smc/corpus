# Analyze Word Frequency

First, cleanup the file :

```
sed -i -E -f corpora-cleanup.sed *.txt
```

Make `report.txt` with the analysis :

```bash
# For matching only Malayalam & ZWJ+ZWNJ. Malayalam unicode block 0x0D00 - 0x0D7F
CHARS=$(python3 -c 'print("".join(map(chr, list(range(0x0D00, 0xD7F + 1)) + [0x200C, 0x200D])))')

cat *.txt | \
    sed 's/[^'"$CHARS"']/\n/g' | \
    sed '/^[[:space:]]*$/d' | \
    tr -d "\r" | \
    sort -bif | \
    uniq -c | \
    sort -gr | \
    awk '{ print $2 " " $1}' \
    > report
```

The output `report` will have format :

```
ഞാൻ 107
ഒരു 70
അത് 45
ആർതർ 43
എന്റെ 42
```

To combine results from multiple reports (`report1` & `report2`) :

```
awk '{ count[$1] += $2 } END { for(elem in count) print elem, count[elem] }' report1 report2 | sort -gr -t " " -k 2 > report
```