
#### Create a subdomain list

1) Use subfinder and assetfinder to create lists passively
```
sudo apt install subfinder
sudo apt install assetfinder
```
```
subfinder -d domain.com > subf_list.txt
```
```
assetfinder -subs-only domain.com > asset_list.txt
```

2) Merge the two lists
```cli
cat asset_list.txt subf_list.txt | sort | uniq > master_sub_list.txt
```

3) Check which ones are active
```
httpx-toolkit -r master_sub_list.txt -sc 200
```





