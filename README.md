# level-merkle-test

Testing [leveldb](https://github.com/rvagg/levelup) replication using
[level-merkle](https://github.com/dominictarr/level-merkle) for a chat like
application.

## 2 party replication

`A - B`

### Desired output

```
$ node test.js 2
 A id: 1
 A 1382016667906.0852: 00
 A 1382016667906.3828: 01
 A 1382016667906.3984: 02
 A 1382016667906.5440: 03
 A 1382016667906.5872: 04
 B id: 2
 A 1382016667906.0852: 00
 A 1382016667906.3828: 01
 A 1382016667906.3984: 02
 A 1382016667906.5440: 03
 A 1382016667906.5872: 04
!A 0
 A 1382007026810: 0
 B 1382007026810: 0
!B 1
 B 1382007028811: 1
 A 1382007028811: 1
!A 2
 A 1382007030814: 2
 B 1382007030814: 2
!B 3
 B 1382007032816: 3
 A 1382007032816: 3
!A 4
 A 1382007034817: 4
 B 1382007034817: 4
!B 5
 B 1382007036820: 5
 A 1382007036820: 5
!A 6
 A 1382007038822: 6
 B 1382007038822: 6
!B 7
 B 1382007040824: 7
 A 1382007040824: 7
!A 8
 A 1382007042825: 8
 B 1382007042825: 8
!B 9
 B 1382007044826: 9
 A 1382007044826: 9
```

### Actual output

```bash
$ node test.js 2
 A id: 1
 A 1382016667906.0852: 00
 A 1382016667906.3828: 01
 A 1382016667906.3984: 02
 A 1382016667906.5440: 03
 A 1382016667906.5872: 04
 B id: 2
!A 0
 A 1382007026810: 0
!B 1
 B 1382007028811: 1
 B 1382007026810: 0
 B 1382007026810: 0
 A 1382007028811: 1
 A 1382007028811: 1
!A 2
 A 1382007030814: 2
 B 1382007030814: 2
!B 3
 B 1382007032816: 3
 A 1382007032816: 3
!A 4
 A 1382007034817: 4
!B 5
 B 1382007036820: 5
 A 1382007036820: 5
 B 1382007034817: 4
!A 6
 A 1382007038822: 6
 B 1382007038822: 6
!B 7
 B 1382007040824: 7
 A 1382007040824: 7
!A 8
 A 1382007042825: 8
 B 1382007042825: 8
```

## 3 party replication

`A - B - C`

## Desired output

```bash
$ node test.js 3
 A id: 1
 A 1382016667906.0852: 00
 A 1382016667906.3828: 01
 A 1382016667906.3984: 02
 A 1382016667906.5440: 03
 A 1382016667906.5872: 04
 B id: 2
 A 1382016667906.0852: 00
 A 1382016667906.3828: 01
 A 1382016667906.3984: 02
 A 1382016667906.5440: 03
 A 1382016667906.5872: 04
 C id: 3
 A 1382016667906.0852: 00
 A 1382016667906.3828: 01
 A 1382016667906.3984: 02
 A 1382016667906.5440: 03
 A 1382016667906.5872: 04
!A 0
 A 1382007331801: 0
 B 1382007331801: 0
 C 1382007331801: 0
!B 1
 B 1382007333802: 1
 A 1382007333802: 1
 C 1382007333802: 1
!C 2
 C 1382007335804: 2
 A 1382007335804: 2
 B 1382007335804: 2
!A 3
 A 1382007337805: 3
 B 1382007337805: 3
 C 1382007337805: 3
!B 4
 B 1382007339807: 4
 A 1382007339807: 4
 C 1382007339807: 4
!C 5
 C 1382007341810: 5
 B 1382007341810: 5
 A 1382007341810: 5
```

## Actual output

```bash
$ node test.js 3
 A id: 1
 A 1382016667906.0852: 00
 A 1382016667906.3828: 01
 A 1382016667906.3984: 02
 A 1382016667906.5440: 03
 A 1382016667906.5872: 04
 B id: 2
 C id: 3
!A 0
 A 1382007331801: 0
!B 1
 B 1382007333802: 1
 A 1382007333802: 1
 B 1382007331801: 0
 B 1382007331801: 0
 A 1382007333802: 1
!C 2
 C 1382007335804: 2
 B 1382007335804: 2
 B 1382007335804: 2
 C 1382007331801: 0
1382007333802: 1
 C 1382007331801: 0
1382007333802: 1
1382007331801: 0
1382007333802: 1
 A 1382007335804: 2
!A 3
 A 1382007337805: 3
 B 1382007337805: 3
 C 1382007337805: 3
!B 4
 B 1382007339807: 4
 A 1382007339807: 4
 C 1382007339807: 4
!C 5
 C 1382007341810: 5
 B 1382007341810: 5
 A 1382007341810: 5
```
