# Wächter von außen

Prüft alle 30 Minuten von außerhalb Vercels, ob das Master Dashboard antwortet und ob seine Zeitpläne (Seiten-Wächter,
Morgenbericht) rechtzeitig laufen. Ablauf: [`.github/workflows/puls.yml`](.github/workflows/puls.yml).

- **Grün:** die Puls-Adresse antwortet 200.
- **Rot:** 503 (ein Zeitplan ist zu lange still) oder keine Antwort (Vercel weg). Der Lauf schlägt fehl, GitHub
  schickt eine Mail; mit den Repo-Geheimnissen `TELEGRAM_BOT_TOKEN` und `TELEGRAM_CHAT_ID` auch eine
  Telegram-Nachricht — nur beim Wechsel, nicht bei jedem Lauf.
- **Öffentlich mit Absicht:** Standard-Runner sind in öffentlichen Repos gratis. Im Code steht kein Geheimnis.
- **Wer bewacht diesen Wächter?** Das Master Dashboard merkt sich jeden Besuch (mit `PULS_SCHLUESSEL`) und zeigt auf
  der Team-Seite und im Morgenbericht, wenn er ausbleibt. GitHub schaltet Zeitpläne in öffentlichen Repos nach
  60 Tagen ohne Änderung ab — dann wieder einschalten (`gh workflow enable puls.yml`).
