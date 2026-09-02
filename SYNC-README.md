# Claude Code skill/agent/command sinxronizatsiyasi

Bu repo `~/.claude` ichidagi **skills/**, **commands/**, **agents/**, **projects/*/memory/**
va **plugins/known_marketplaces.json** ni sinxron saqlaydi. Runtime fayllar, sessiyalar,
telemetriya va maxfiy `engagements/` ma'lumotlari `.gitignore` orqali chetlatilgan.

## Birinchi marta (SHU qurilmada) — remote yaratib push qilish
GitHub'da shaxsiy (private) repo oching, masalan `claude-config`, keyin:

    cd ~/.claude
    git remote add origin git@github.com:<FOYDALANUVCHI>/claude-config.git
    git branch -M main
    git push -u origin main

## Boshqa qurilmada — birinchi marta olish
    # Agar u yerda ~/.claude bo'lsa, avval zaxira: mv ~/.claude ~/.claude.bak
    git clone git@github.com:<FOYDALANUVCHI>/claude-config.git ~/.claude
    # Agar ~/.claude allaqachon mavjud bo'lsa (Claude Code o'rnatilgan):
    #   cd ~/.claude && git init && git remote add origin <url> && git fetch && git checkout -f main

## Har kunlik ishlatish
    # o'zgarishni yuborish:
    cd ~/.claude && git add -A && git commit -m "update" && git push
    # boshqa qurilmadagi yangilikni olish:
    cd ~/.claude && git pull
