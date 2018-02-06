tcplstat - TCP�����ع���
==========================

<!-- TOC -->

- [1. ����](#1-����)
- [2. ��װ](#2-��װ)
    - [2.1. Դ����밲װ](#21-Դ����밲װ)
- [3. ʹ��](#3-ʹ��)
    - [3.1. �����в���˵��](#31-�����в���˵��)
    - [3.2. һ��ʾ������ʱ���TCP�����¼���](#32-һ��ʾ����ʱ���tcp�����¼�)
    - [3.3. ��һ��ʾ���������ӶϿ������ͳ����Ϣ��](#33-��һ��ʾ�������ӶϿ������ͳ����Ϣ)
    - [3.4. ��һ��ʾ�����ɼ�ͳ��SQL��ʱ��](#34-��һ��ʾ���ɼ�ͳ��sql��ʱ)
- [4. ���](#4-���)

<!-- /TOC -->

# 1. ����

ֻ��Ϊ���������ϲ�С�Ŀ���һ��libpcap���ϣ��ҵĴ�����ڴ��������������ĸ����Ϸ������飬�������ܶ�������ڵ��������TCP�����ع��ߡ�

tcplstat�ǻ���libpcap������̽������������ع��ߣ�����**��·**�������о��������豸���˹����TCP���ݣ����ٵ�ǰ����TCP���ӻỰ����¼���о�����TCP���飬�����ӶϿ��򵽴�����¼��ʱ����ͳ����Ϣ���������������������������ַ������ʱ������������ָ������ӳ١��Ĳ����ָ������ӳ٣����ݷ�����ϸ������������ӳٺ��෴��������ӳٵ���С��ƽ�������ͳ��ֵ��

tcplstat��**��·**���������Բ����Ӧ������κ�Ӱ�죬Ҳ��������Ӧ�ã����ɻ��������������������ϸ��ͳ����Ϣ��

tcplstat��ʵ�ֻ��������ع���ʱ��ʵ���˲ɼ�����SQL��ʱ��Ϣ��ͬ��Ҳ��**��·**���񣬲�Ӱ��Ӧ��Ҳ�������Ӧ�ã�����Ӧ���Ż����ܡ�

tcplstat�ǿ�Դ�ģ�����������Linux�ں˵ĺ����������Դ���⣬����Դ��ֻ��1500�����ң�Դ��ṹ���׶���

# 2. ��װ

��������tcplstat���԰�װ���κ���libpcap�Ļ���������Linux��WINDOWS��AIX�ȣ�������Linux����ϵͳΪ����

## 2.1. Դ����밲װ

��tcplstatԴ���й�վ�㣨��ַ�������������Դ������⿪������Դ��Ŀ¼

```
$ tar xvzf tcplstat.tar.gz
...
�� cd tcplstat/src
```

�����޸İ�װĿ¼

```
$ vi makeinstall
_BINBASE        =       $(HOME)/bin
```

**ע�⣺���뻷����Ҫ������libpcap-delvel����Ԥ�Ȱ�װ�á�**

���롢��װtcplstat

```
$ make -f makefile.Linux
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c list.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c rbtree.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c rbtree_ins.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c Util.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c main.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c PcapCallback.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c ProcessTcpPacket.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c AddTcpPacket.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -I/home/calvin/include -I. -I/home/calvin/include  -c OutputTcplSession.c
gcc -g -fPIC -O2 -Wall -Werror -fno-strict-aliasing -o tcplstat list.o rbtree.o rbtree_ins.o Util.o main.o PcapCallback.o ProcessTcpPacket.o AddTcpPacket.o OutputTcplSession.o -L/home/calvin/lib -L. -L/home/calvin/lib -lpcap 
$ make -f makefile.Linux install
cp -rf tcplstat /home/calvin/bin/
```

��������ֻ������һ����ִ�г���`tcplstat`��Ҳ�����и��Ƶ�Ŀ��Ŀ¼��

��ʾ�汾��Ϣ

```
$ tcplstat -v
tcplstat v0.5.0 build Feb  6 2018 22:40:44
copyright by calvin<calvinwilliams@163.com> 2018
```

# 3. ʹ��

## 3.1. �����в���˵��

���������в���ִ����ʾ���������в���

```
$ tcplstat
USAGE : tcplstat -v
                 -l
                 [ -i (network_interface) ] [ -f (filter_string) ] [ -o [ESPDd] ] [ --sql ] [ --log-file (pathfilename) ]
-o E : Output EVENT
   S : Output SESSION
   P : Output PACKET
   D : Output PACKET DATA
   d : Output DEBUG
--sql : Output SQL time elapse
NOTICE : See pcap-filter(7) for the syntax of filter
```

* `-i`���������豸�ӿڣ���������Ĭ��ʹ��`any`
* `-f`����������˹��򣬱���`tcp port 445`��̽�������ӵ��˿�445������TCP���飬����μ�`pcap-filter(7)`
* `-o`һ������TCP���飬����������ͣ�E��ʾ��������¼���S��ʾ���ӶϿ�����Ựͳ����Ϣ��P��ʾ���ӶϿ����TCP����ͳ����Ϣ��D��ʾ���ӶϿ����TCP����������Ϣ��d��ʾ���������Ϣ
* `--sql`����SQLͳ�ƺ�ʱ��Ϣ
* `--log-file`һ������TCP���飬�������־�ļ����������ļ����������Ļ

**ע�⣺ִ��tcplstat��ҪrootȨ�ޡ�**

## 3.2. һ��ʾ������ʱ���TCP�����¼���

��һ������tcplstat

```
# tcplstat -f "tcp port 445" -o E
```

�ڶ�����445�˿ڷ���һ���ַ�����Ȼ��samba����������ǿ�жϿ�

```
$ echo "hello" | nc 114.215.179.129 445
```

��һ�����

```
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[36893] DSTPORT[445] SEQ[1991766964] ACKSEQ[0] SYN[1] ACK[0] FIN[0] PSH[0] RST[0] URG[0] | [0]bytes
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[445] DSTPORT[36893] SEQ[857579400] ACKSEQ[2008544180] SYN[1] ACK[1] FIN[0] PSH[0] RST[0] URG[0] | [0]bytes
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[36893] DSTPORT[445] SEQ[2008544180] ACKSEQ[874356616] SYN[0] ACK[1] FIN[0] PSH[0] RST[0] URG[0] | [0]bytes
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[36893] DSTPORT[445] SEQ[2008544180] ACKSEQ[874356616] SYN[0] ACK[1] FIN[0] PSH[1] RST[0] URG[0] | [6]bytes
E |                  0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F    0123456789ABCDEF
E |     0x00000000   68 65 6C 6C 6F 0A                                 hello.          
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[445] DSTPORT[36893] SEQ[874356616] ACKSEQ[2109207476] SYN[0] ACK[1] FIN[0] PSH[0] RST[0] URG[0] | [0]bytes
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[36893] DSTPORT[445] SEQ[2109207476] ACKSEQ[874356616] SYN[0] ACK[1] FIN[1] PSH[0] RST[0] URG[0] | [0]bytes
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[445] DSTPORT[36893] SEQ[874356616] ACKSEQ[2125984692] SYN[0] ACK[1] FIN[1] PSH[0] RST[0] URG[0] | [0]bytes
E | LHT[113] | SRCMAC[] DSTMAC[] | SRCIP[114.215.179.129] DSTIP[114.215.179.129] | SRCPORT[36893] DSTPORT[445] SEQ[2125984692] ACKSEQ[891133832] SYN[0] ACK[1] FIN[0] PSH[0] RST[0] URG[0] | [0]bytes
```

E��ͷ����Ϊһ��TCP���飬�����з��ͷ�IP�����շ�IP�����ͷ�PORT�����շ�PORT���������ͱ�־������������ݴ�С����Ϣ��

## 3.3. ��һ��ʾ���������ӶϿ������ͳ����Ϣ��

��һ������tcplstat

```
tcplstat -f "tcp port 445" -o SPD
```

�ڶ�����445�˿ڷ���һ���ַ�����Ȼ��samba����������ǿ�жϿ�

```
$ echo "hello" | nc 114.215.179.129 445
```

��һ�����

```
S | [114.215.179.129:36911]->[114.215.179.129:445] | 1517929072.239805 | 0.029388 | 0.000017 0.000014 , 0.000007 0.000482 0.000957 0.000971 0.000489 0.000971 , 0.000035 0.028340 0.000018 | 2 6
P |     1517929072.239805 | 0.000000 0.000000 | [114.215.179.129:36911]->[114.215.179.129:445] | S..... 0
P |     1517929072.239822 | 0.000017 0.000017 | [114.215.179.129:36911]<-[114.215.179.129:445] | S..A.. 0
P |     1517929072.239836 | 0.000014 0.000014 | [114.215.179.129:36911]->[114.215.179.129:445] | ...A.. 0
P |     1517929072.240793 | 0.000957 0.000971 | [114.215.179.129:36911]->[114.215.179.129:445] | ..PA.. 6
D |                  0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F    0123456789ABCDEF
D |     0x00000000   68 65 6C 6C 6F 0A                                 hello.          
P |     1517929072.240800 | 0.000007 0.000007 | [114.215.179.129:36911]<-[114.215.179.129:445] | ...A.. 0
P |     1517929072.240835 | 0.000035 0.000035 | [114.215.179.129:36911]->[114.215.179.129:445] | .F.A.. 0
P |     1517929072.269175 | 0.028340 0.028340 | [114.215.179.129:36911]<-[114.215.179.129:445] | .F.A.. 0
P |     1517929072.269193 | 0.000018 0.000018 | [114.215.179.129:36911]->[114.215.179.129:445] | ...A.. 0
```

S��ͷ����Ϊһ������ͳ����Ϣ�������з��ͷ�IP��PORT�����շ�IP��PORT����������ʱ����������ܴ���ʱ�䡢�������ָ������ӳ١��Ĳ����ָ������ӳ٣����ݷ�����ϸ������������ӳٺ��෴��������ӳٵ���С��ƽ�������ͳ��ֵ��

P��ͷ����Ϊһ�������е�һ��TCP����ͳ����Ϣ����������ʱ���������������ӳٺ��෴��������ӳٵ���Ϣ��

���Կ������Լ�����ʲô�������ݣ�����������в���`-o`�������ĸ���ϼ��ɣ�����ϸ����Ϣ���������

```
# tcplstat -f "tcp port 445" -o ESPDd
```

## 3.4. ��һ��ʾ�����ɼ�ͳ��SQL��ʱ��

����SQL��ԭ��ܼ򵥣����ÿһ��TCP�������Ƿ����SQL��䣬�������������ǣ��ȴ���һ����Ч�غɵķ���TCP���鵽���󣬼���ʱ����SQLִ��ʱ�䡣

������PostgreSQLΪ����MySQL��Oracle��ͬ����Ч��

��һ������tcplstat

```
tcplstat -f "tcp port 8432" --sql
```

�ڶ�����psql�����ݿ�����

```
calvin=# \d
                               �����б�
 �ܹ�ģʽ |                   ����                   |  �ͱ�  | ӵ���� 
----------+------------------------------------------+--------+--------
 public   | alphastock_company_info                  | ���ϱ� | calvin
 public   | alphastock_company_ipo                   | ���ϱ� | calvin
 public   | alphastock_stock_code                    | ���ϱ� | calvin
 public   | alphastock_stock_kline                   | ���ϱ� | calvin
 public   | alphastock_stock_kline_max_closing_price | ���ϱ� | calvin
 public   | financing_chinawealth                    | ���ϱ� | calvin
 public   | whoispider_domain                        | ���ϱ� | calvin
(7 �м�¼)

calvin=# select count(*) from alphastock_company_info;
 count 
-------
  3596
(1 �м�¼)

calvin=# select count(*) from alphastock_company_ipo ;
 count 
-------
  3596
(1 �м�¼)

calvin=# select count(*) from alphastock_stock_code ;
 count 
-------
  3596
(1 �м�¼)

calvin=# select count(*) from alphastock_stock_kline ;
  count  
---------
 8826375
(1 �м�¼)

calvin=# select count(*) from financing_chinawealth ;
calvin-# ;
 count  
--------
 168148
(1 �м�¼)
```

��һ�����

```
Q | 0.002280 select count(*) from alphastock_company_info;
Q | 0.122536 select count(*) from alphastock_company_ipo ;
Q | 0.001183 select count(*) from alphastock_stock_code ;
Q | 41.287111 select count(*) from alphastock_stock_kline ;
Q | 3.148893 select count(*) from financing_chinawealth ;
```

Q��ͷ����Ϊһ��SQL��ʱͳ�ƣ����Կ�����`alphastock_stock_kline`�ܴ�SQL`select count(*) from alphastock_stock_kline`����41�룬��`alphastock_company_ipo`��С��SQL`select count(*) from alphastock_company_ipo`����0.1�롣

�����ɼ�ͳ�ƹ�����ȫ��**��·**��ʽ���У���Ӱ��Ӧ��Ҳ��������Ӧ�á�

# 4. ���

��ӭʹ��tcplstat�������ʹ��������������������ң�лл ^_^

Դ���йܵ�ַ : [��Դ�й�](https://gitee.com/calvinwilliams/tcplstat)��[github](https://github.com/calvinwilliams/tcplstat)

�������� : [����](mailto:calvinwilliams@163.com)��[Gmail](mailto:calvinwilliams.c@gmail.com)
