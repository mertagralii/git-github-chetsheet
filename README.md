
# Git Yardım Seçenekleri:

Öğrenebileceğiniz en önemli Git komutu git help'tir.

Hiçbir seçenek olmadan git help komutunu çalıştırdığınızda, sık kullanılan komutlar için çeşitli bölümlerle birlikte git komutunun harika bir özetini göreceksiniz:
```bash
usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]
```

Bunlar çeşitli durumlarda kullanılan yaygın Git komutlarıdır
```bash
bir çalışma alanı başlatın (Ayrıca bakınız: git help tutorial)
   clone      Bir depoyu yeni bir dizine klonlama
   init      Boş bir Git deposu oluşturma veya mevcut bir depoyu yeniden başlatma

...
```

Yardım özetinin altında, son derece yararlı olan iki ek komut göreceksiniz: git help -a ve git help -g:

`git help -a` ve `'git help -g'` mevcut alt komutları ve bazı kavram kılavuzlarını listeler.

`git help -g` komutunu çalıştırdığınızda bir öğretici listesi alırsınız. Örneğin, everyday günlük Git için bir dizi komuttur.

`git help -a` komutunu çalıştırırsanız, tüm alt komutların bir listesini alırsınız.

Belirli bir alt komutun kullanım talimatlarını almak için `git help` alt komutunu çalıştırabilirsiniz, örneğin: `git help init`

Bir alt komutu aramak için `/subcommand` yazın ve enter tuşuna basın. Geri gitmek için `shift + N` ve ileri gitmek için `N` tuşlarını kullanın. Çıkmak için `Q` tuşuna basın.

# `git init` ile Git Deposu Oluşturma : 

`git init` yeni bir git deposu oluşturmak için kullanılan komuttur. Bir depoyu yeni bir dizinde başlatmak için isteğe bağlı bir yol girin:
```bash
git init my-git-notes
```
cd my-git-notes ile dizine geçin, ardından `ls`'yi çalıştırın ve dizinin boş göründüğünü görün.
Ancak, `ls -a ` çalıştırıldığında gizli bir `.git` dizini olduğu ortaya çıkar:
```bash
$~/my-git-notes> ls -a

.git
```
.git dizininin içeriğini listelemek için `ls .git` kullanabilirsiniz:

![image](https://github.com/user-attachments/assets/05c6fa4e-ebf7-49b0-9138-6e29989db453)

İç içe geçmiş klasör ve dosyaların bulunduğu bu .git dizini, normal sistem dizinini bir git deposuna dönüştüren şeydir.

Daha fazla git init seçeneği ve bilgi için `git help init` yazın.

# Git Durumu ve Gizli .git Dizini

`git status`, Git depoları ile çalışırken her zaman kullanacağınız bir komuttur.

Bu komut bulunduğunuz dalı ve işlem geçmişinizi gösterecektir.

Depomuz yeni olduğu için görülecek fazla bir şey yok:
```bash
$ git status

On branch main
No commits yet
nothing to commit (create/copy files and use "git add" to track)
```
Bu işlevsellik, depomuzdaki gizli .git dizini tarafından desteklenmektedir. Peki bu dizini kaldırırsak ne olur?
```bash
$ rm -vrf .git
```
Şimdi, `git status`'u çalıştırdığımızda, artık çalışmıyor çünkü bu artık bir depo değil, sadece bir klasör.
```bash
$ git status

fatal: not a git repository (or any of the parent directories): .git
```
Olduğumuz yere geri dönmek için dizin içinde `git init`'i tekrar çalıştırın:
```bash
git init
```
# Git İzleme ve Hazırlama Dosyaları
Bir önceki dersimizde depomuzun içinde `git status`'u çalıştırdığımızda, işlenecek bir şey olmadığı ve dosyaları oluşturup eklememiz gerektiği söylendi. Öyleyse bunu yapalım!

`echo` ile Dosya Oluşturma
`echo` komutu yeni dosyalara metin yazmak için kullanılabilir.

Aşağıdaki komutlar `git-help.txt`, `git-init.txt` ve `git-status.txt` için yeni dosyalar oluşturacaktır:
```bash
echo "#git-help" > git-help.txt
echo "#git-init" > git-init.txt
echo "#git-status" > git-status.txt
```
`ls`'yi çalıştırmak bize dosyaların oluşturulduğunu gösterecektir.

Dosya Durumunu Kontrol Edin

`git status` çalıştırıldığında izlenmemiş dosyalar olduğu görülüyor:
```bash
$ git status

On branch main
No commits yet
Untracked files:
(use "git add <file>..." to include in what will be committed)
git-help.txt
git-init.txt
git-status.txt
nothing added to commit but untracked files present (use "git add" to track)
```
Dosyaları takip etmek için önce onları eklememiz gerekir.

Dosya Ekleme
Dosyaları dosya adı ile birlikte `git add` komutu ile ekleyebiliriz.

Önce `git-help.txt` dosyasını ekleyelim:
```bash
git add githelp.txt
```
`git status`'u tekrar çalıştırdığımızda, "işlenecek değişiklikler" adlı ek bir bölümümüz var:
```bash
$ git status

On branch main
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   git-help.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git-init.txt
        git-status.txt

```
`git-help.txt` değişikliklerinin henüz işlenmediğini ancak işlenmek üzere hazırlandığını unutmayın.

Geri Kalan Dosyaları Aşama Aşama Ekleyin
Geri kalan dosyalar git add ile tek tek eklenebilir.

Ancak, `git add .` kısayolunu kullanmak, dizine eklenmemiş her şeyi ekleyecektir.

Geri kalan dosyaları ekledikten sonra `git status`'u son bir kez çalıştırdığımızda her şeyin dizinimize taşındığını ve commit için hazırlandığını göreceğiz.

# Hazırlama Alanınızı Hassaslaştırmak için `git reset` Kullanımı

Bir commit oluşturmadan önce, yalnızca dahil etmek istediğimiz dosyaların ve değişikliklerin dizinde veya aşamalı alanda olduğundan emin olmak isteriz.

Bir dosyayı commit'ten kaldırmak için dosya adıyla birlikte `git reset` komutunu kullanabilirsiniz:

git reset git-status.txt

Komutu çalıştırdıktan sonra, dosyanın aşamalı alandan kaldırıldığını doğrulamak için git status'u tekrar kullanabilirsiniz.
```bash
$ git status

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   git-help.txt
        new file:   git-init.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git-status.txt
```
Daha önce olduğu gibi, `get reset .` tüm dosyaları sahnelenen alandan kaldıracaktır. Bu, işlem yapmadan önce amaçlanan dosyaları gözden geçirmenize ve aşamalandırmanıza olanak tanır.

Commits için Git Yapılandırmasını Ayarlama

Herhangi bir şey işlemeden önce, bazı git yapılandırmaları eklemeniz gerekir. Paylaşımlı bir makinede olmadığınızı varsayarsak, bunu global olarak ekleyebilirsiniz.

Taahhütlerinizde görünmesini istediğiniz bir kullanıcı adı ve bir kullanıcı e-posta adresi eklemeniz gerekir.

Bu komutlarla kullanıcı adınızı ve e-postanızı ayarlamak için `config komutunu --global bayrağı ile kullanın`:
```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@address.com"
```
İstediğiniz zaman list bayrağını kullanarak git yapılandırmanızı görebilirsiniz:
```bash
git config --list
```
Bu komut, bazı sistem varsayılanlarının yanı sıra sağladığınız iki seçeneği de görüntüleyecektir. Bir kullanıcı ve e-posta ile artık taahhütlerinizi imzalamaya hazırsınız.

# Git Commit, Add ve Status'u Anlama

`Git commit` komutu bir commit yapmak için kullanılır. Commit'ler, `-m` bayrağı ile eklenen bir mesaj gerektirir.

Şimdiki zaman kipinde taahhüt mesajları kullanmak iyi bir uygulamadır:
```bash
git commit -m "Yardım, başlangıç ve durum notları ekleyin"
```
Commit komutu bittikten sonra, dalı, kısaltılmış commit SHA'sını ve yazdığımız mesajı gösterecektir:
```bash
$ git commit -m "Add help, init, and status notes"

[main (root-commit) 1e3b9b0] Add help, init, and status notes
 3 files changed, 3 insertions(+)
 create mode 100644 git-help.txt
 create mode 100644 git-init.txt
 create mode 100644 git-status.txt
```
İşlenecek herhangi bir dosya yoksa, commit komutunun aslında bir commit yapmak yerine durum çıktısını döndüreceğini unutmayın.

Başarılı bir işlemden sonra `git status` tekrar çalıştırıldığında işlenecek bir şey olmadığını ve temiz bir çalışma ağacımız olduğunu bildirecektir:
```bash
$ git status

On branch main
nothing to commit, working tree clean
```
# Commit Geçmişini git show ile İnceleme

`git show`, commitlerinizi incelemenizi sağlayan bir komuttur. Herhangi bir argüman olmadan kullanıldığında, commit'in oluşturduğu tam fark da dahil olmak üzere en son commit'i görüntüler:
```bash
$ git show

commit 1e3b9b0061712908132409ssdf234 (HEAD -> main)
Author: Your Name <youremail@address.com>
Date: Mon Jan 1 00:00:00 2021 -0400

    Add help, init, and status notes

diff --git a/git-help.txt b/git-help.txt
new file mode 100644
index 0000000..e69de29
--- /dev/null
+++ b/git-help.txt
@@ -0,0 +1 @@
+#git-help
diff --git a/git-init.txt b/git-init.txt
new file mode 100644
index 0000000..23b0b9e
```
Klavyenizdeki `q` tuşuna basarak bu görünümden çıkabilirsiniz.

`Git show` ile commit SHA'sını kullanarak da açık olabilirsiniz. Tam shaw ya da kısaltılmış altı karakterli versiyonu kullanabilirsiniz:
```bash
git show 1e3b9b
```
İncelemek istediğiniz commit ana dalın başındaysa, commit `SHA` yerine `HEAD` takma adını kullanabilirsiniz:
```bash
git show HEAD
```
Bu komutlar yukarıdaki örnekte olduğu gibi aynı bilgileri gösterecektir.

# Etkileşimli Git Evreleme

Yeni bir komut öğrenmeden önce, şu ana kadar ele aldığımız git alt komutlarını uygulamak için hızlı bir alıştırma yapalım.

Git durumunu kontrol et

`git status`'ü çalıştırdığımızda, henüz işlenmek üzere hazırlanmamış birkaç dosyamız olduğunu görüyoruz:
```bash
$ git status

On branch main
Untracked files:
(use "git add <file>..." to include in what will be committed)
git-add.txt
git-commit.txt
git-config.txt
git-log.txt
git-reset.txt
git-show.txt
```
Ekle ve Taahhüt Et

`git-add.txt` ve `git-reset.txt` dosyalarını ekleyelim:
```bash
git add git-add.txt git-reset.txt
```
Sonra bunları işleyecek ve bir mesaj ekleyeceğiz:
```bash
git commit -m "Add stagingi subcommand notes"
```
Taahhüt mesajında bir yazım hatası yaptığımıza dikkat edin!

Taahhüt Mesajını Değiştirme :

En son commit mesajını `git commit --amend` ile düzeltebiliriz:
```bash
git commit --amend
```
Bu, mesajı düzenlemek için terminal metin düzenleyicisini (genellikle Vim) açacaktır:

`Vim`'de, hatalı karaktere gitmek için ok tuşlarını kullanın, silmek için `x` tuşuna basın ve ardından kaydetmek ve çıkmak için `:wq` yazın.

Düzeltilmesi gereken tek bir karakterden daha fazlası varsa, Vim'in ekleme moduna girmek ve mesajı düzeltmek için `i`'yi kullanabilirsiniz. Ekleme modundan çıkmak için `escape` tuşuna basın ve kaydetmek ve çıkmak için `:wq` yazın.

`git show` ile komutları görün

Terminale döndüğünüzde, son commit'i görmek ve mesajın düzeltildiğini doğrulamak için `git show`'u çalıştırın.

Önceki commitleri kontrol etmek için `git show head^` komutunu kullanın, bu bize son committen önceki commitleri gösterecektir. Buradaki ^, head'e eklenen ve bir önceki commit'i istediğimizi belirten göreceli bir referanstır:
```bash
git show head^
```
Bu durumda, git-help.txt, git-init.txt ve git-status.txt dosyalarını eklediğimiz önceki commit'i göreceğiz.

`q` tuşuna basarak commit görünümünden çıkabilirsiniz.

Kalan Dosyaları Aşamalandırın ve İşleyin
Şimdi kalan dosyaları `git add` ile aşamalandıralım:
```bash
$ git add .

On branch main
Changes to be committed:
(use "git restore --staged <file>..." to unstage)
new file: git-commit.txt
new file: git-config.txt
new file: git-log.txt
new file: git-show.txt
```
git-config.txt dosyası komutlar üzerinde değil git yapılandırması üzerinde çalıştığından, bu dosyayı diğer komutlardan ayrı tutmak istiyoruz.

Bir Dosyanın Sahnesini Kaldırma

git-config.txt dosyasını kaldırmak için `git reset`'i kullanın:
```bash
git reset git-config.txt
```
Alternatif olarak, `git reset` ile tüm dosyaların aşamasını kaldırabilirsiniz. daha sonra işlemeniz gerekenleri geri ekleyebilirsiniz.

Çeşitli git alt komutlarını kullanarak bir dosyayı başarıyla sahneledik, işledik, bir commit mesajını düzelttik ve sahnelemeyi kaldırdık, ancak

Joker Karakter Olarak Dize Globları Kullanın
Tam dosya adını yazmaktan sıkıldıysanız, bir dosyayı tanımlamak için bir dize globu kullanabilirsiniz.

Örneğin, get-config.txt dosyasını aşağıdaki şekilde hedefleyebiliriz:
```bash
git add '_con_'
```
con alt dizesi git-config.txt dosyası için benzersiz olduğundan, eklenen tek dosya olacaktır.

Dosya eklendikten sonra değişiklikleri işleyebiliriz:
```bash
git commit -m "Add username and email config"
```
İnteraktif Modda Dosya Ekleme
Kalan dosyaları eklemek için `git add`'i `interaktif` modda kullanalım:
```bash
git add -i
```
Bu mod, tüm komutlarımızı git ile öncelemek zorunda kalmadan hazırlama alanıyla etkileşime girmemizi sağlar:

![image](https://github.com/user-attachments/assets/79b93582-6f52-4e4a-b5d0-2f7f98e2ecce)

"Şimdi ne olacak?" boşluğuna, kullanmak istediğiniz ilgili komutun harfini yazın.

Biz "`add untracked`" kullanmak istiyoruz, bu yüzden `a` gireceğiz.

Şimdi, kalan izlenmemiş dosyaları göreceksiniz. Dosyayı seçmek için numaraları kullanın.

![image](https://github.com/user-attachments/assets/72b38a05-434e-4965-a438-877a64cc3b4a)

İşiniz bittiğinde, "Şimdi ne olacak?" istemine `geri dönmek için tekrar enter tuşuna basın.`

Etkileşimli Modda Durumu Kontrol Edin
`Durumu kontrol etmek için komut istemine s yazın`. Üç dosyanın şu anda aşamalı olduğunu gösterecektir:
```bash
What now> s
staged unstaged path
1: +1/-0 nothing git-commit.txt
2: +1/-0 nothing git-log.txt
3: +1/-0 nothing git-show.txt
```
`Gerekirse komut istemine r girerek değişiklikleri geri alabilirsiniz.`

Her şey iyi görünüyorsa, `çıkmak için enter` tuşuna basın ve `etkileşimli moddan çıkmak için q` tuşunu kullanın.

git durumunu kontrol edin ve Commit edin
Etkileşimli moddan çıktıktan sonra git durumu, git add etkileşimli modu ile işlediğimiz her şeyi gösterecektir. Devam edin ve değişiklikleri `git commit -m "Add commit subcommands"` ile işleyin.

Artık commit mesajlarını nasıl düzenleyeceğinizi, dosyaları seçmek için string glob'ları nasıl kullanacağınızı ve git'i interaktif modda nasıl kullanacağınızı öğrendiniz. Bir sonraki komuta geçmeye hazırsınız.

# Daha İyi İş Akışı için Git Günlük Çıktısını Optimize Etme

`git log` komutu deponuzdaki commit'lerin bir listesini gösterir.

Varsayılan olarak, çıktı ayrıntılıdır ve her bir commit hakkında ayrıntılı bilgi gösterir:

![image](https://github.com/user-attachments/assets/ef4903d5-7579-4df8-8b14-38d8c3b80a3c)

`oneline` bayrağını kullanmak, commit geçmişinin daha kısa bir görünümünü verecektir. Bu, her bir SHA'nın ilk 7 karakteri ve mesajı dahil olmak üzere her bir commit için sadece en alakalı bilgileri gösterecektir:
```bash
git log --oneline
```
![image](https://github.com/user-attachments/assets/2a90169c-2e51-49f8-b6c2-7eb25c48ef05)

Bu kısa biçimi beğendiyseniz ve varsayılan ayar olarak kaydetmek istiyorsanız, git yapılandırmanızda `format.pretty` seçeneğini ayarlayarak Git'i her zaman oneline biçimini kullanacak şekilde yapılandırabilirsiniz:
```bash
git config format.pretty oneline
```
İlginç bir şekilde, yapılandırmaya çevrimiçi seçeneğinin eklenmesi, günlük çıktısında tam SHA'nın gösterilmesine neden olur. Kısaltılmış SHA'nın kullanıldığından emin olmak için `log.abbrevCommit `seçeneğini `true` olarak ayarlayın:
```bash
git config log.abbrevCommit true
```
Bu yapılandırma güncellemeleri ile git log güzel ve kısa günlük mesajları görüntüleyecektir.

Hangi seçeneklerin uygulandığını görmek için `git config --list` komutu ile Git yapılandırmanızı inceleyebilirsiniz.

