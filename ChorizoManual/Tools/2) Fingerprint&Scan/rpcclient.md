
$ rpcclient -U ""  IP


| **Query** | **Description** |
| ---- | ---- |
| `srvinfo` | Server information. |
| `enumdomains` | Enumerate all domains that are deployed in the network. |
| `querydominfo` | Provides domain, server, and user information of deployed domains. |
| `netshareenumall` | Enumerates all available shares. |
| `netsharegetinfo <share>` | Provides information about a specific share. |
| `enumdomusers` | Enumerates all domain users. |
| `queryuser <RID>` | Provides information about a specific user. |
|  |  |

To Brute Force User ID's:
```shell-session
$ for i in $(seq 500 1100);do rpcclient -N -U "" 10.10.10.10 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```