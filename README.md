OverTheWire
Bandit
lvl0
> ssh -p 2220 bandit0@bandit.labs.overthewire.org
> pega o readme que tá na home, flag é senha pro lvl1
FLAG: boJ9jbbUNNfktd78OOpsqOltutMc3MY1

lvl1
arquivo na home nomeado como "-"
cat e ele não rola
> cat /home/bandit1/- para ler
FLAG: CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

lvl2
senha em arquivo "spaces in this filename"
> cat spaces\ in\ this\ filename
FLAG: UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

lvl3
senha em arquivo oculto dentro do inhere/
> ls --all inhere/
> cat inhere/.hidden
FLAG: pIwrPrtPN36QITSp3EQaw936yaFoFgAB

lvl4
senha está no único arquivo human-readable do diretório inhere/
> file /home/bandit4/inhere/TODOS-ARQS
> cat /home/bandit4/inhere/-file07
FLAG: koReBOKuIDDepwhWk7jZC0RTdopnAYKh

lvl5
uma pa de diretorio dentro de inhere/ a senha tá em um deles, ela é human-readable; 1033bytes in size; non-executable
> find . -size 1033c ! -executable
FLAG: DXjZPULLxYr17uwoI01bNLQbtFemEgo7

lvl6
a senha tá em algum lugar do servidor, sabemos que:
owned by user bandit7
owned by group bandit6
33 bytes in size
> find / -type f -size 33c -user bandit7 -group bandit6 | grep bandit7
FLAG: HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

lvl7
achar a senha dentro do arquivo data.txt, está próxima da palavra millionth
> grep "millionth" data.txt
FLAG: cvX2JJa4CFALtqS87jk27qwqGhBM9plV

lvl8
Comandos estudados
- grep :: busca string em arquivos ou diretorios e retorna o que encontrou e
linha
- sort :: ordenaçao -r reversa
- uniq :: remove linhas adjacentes com conteudo igual
- strings
- base64
tr
tar
gzip
bzip2
xxd

A senha e a unica linha do arquivo data.txt que nao se repete
> sort data.txt | uniq -c :: e a unica linha com numero 1
FLAG: UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

lvl9
Senha ta no arquivo data.txt, em uma das unicas linhas humam-readable e seguida de muitos -(=)
> strings data.txt | grep "="
FLAG: truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

lvl10
A senha esta no arquivo data.txt criptografada com base64
> base64 -d data.txt
FLAG: IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

lvl 11
senha ta no arquivo data.txt usando ROT13
> cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
FLAG: 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EU0u

lvl12
senha ta no arquivo data.txt, um hexdump que foi comprimido muitas vezes
ir fazendo o caminho reverso
>
bandit12@bandit:/tmp/otropicalista$ cat data.txt | xxd -r > data
bandit12@bandit:/tmp/otropicalista$ file data
data: gzip compressed data, was "data2.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/otropicalista$ mv data data2.gz
bandit12@bandit:/tmp/otropicalista$ gzip -d data2.gz 
bandit12@bandit:/tmp/otropicalista$ file data2
data2: bzip2 compressed data, block size = 900k
bandit12@bandit:/tmp/otropicalista$ mv data2 data3.bz
bandit12@bandit:/tmp/otropicalista$ bzip2 -d data3.bz
bandit12@bandit:/tmp/otropicalista$ ls
data3  data.txt
bandit12@bandit:/tmp/otropicalista$ file data3
data3: gzip compressed data, was "data4.bin", last modified: Thu May  7 18:14:30 2020, max compression, from Unix
bandit12@bandit:/tmp/otropicalista$ mv data3 data4.gz
bandit12@bandit:/tmp/otropicalista$ gzip -d data4.gz 
bandit12@bandit:/tmp/otropicalista$ mv data4 data5.tar
bandit12@bandit:/tmp/otropicalista$ tar -xf data5.tar 
bandit12@bandit:/tmp/otropicalista$ mv data5.bin data6.tar
bandit12@bandit:/tmp/otropicalista$ tar -xf data6.tar 
bandit12@bandit:/tmp/otropicalista$ mv data6.bin data7.bz
bandit12@bandit:/tmp/otropicalista$ bzip2 -d data7.bz
bandit12@bandit:/tmp/otropicalista$ mv data7 data8.tar
bandit12@bandit:/tmp/otropicalista$ tar -xf data8.tar 
bandit12@bandit:/tmp/otropicalista$ mv data8.
data8.bin  data8.tar  
bandit12@bandit:/tmp/otropicalista$ mv data8.bin data9.gz
bandit12@bandit:/tmp/otropicalista$ gzip -d data9.gz 
bandit12@bandit:/tmp/otropicalista$ file data9
data9: ASCII text
bandit12@bandit:/tmp/otropicalista$ cat data9

FLAG: 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

lvl13
a senha esta no arquivo /etc/bandit_pass/bandit14 e so pode ser lida pelo
usuario bandit14. Conseguir ssh pra ver a senhae passar de nivel
> ssh bandit14@localhost -i sshkey.private
FLAG: 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

lvl14
pra pegar a senha, basta enviar para a porta 30000 do localhost a senha que usou para acessar esse nivel
> echo "senha_lvl14" | nc localhost 30000
FLAG: BfMYroe26WYalil77FoDi9qh59eK5xNr

lvl15
para conseguir a senha aqui, mande para a senha do ultimo para a porta 30001 do localhost usando criptografia ssl
> echo "BfMYroe26WYalil77FoDi9qh59eK5xNr" | openssl s_client -connect localhost:30001 -ign_eof

FLAG: cluFn7wTiGryunymYOu4RcffSxQluehd

lvl16
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii







