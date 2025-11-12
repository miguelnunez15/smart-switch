# 🧠 smart-switch

**Un alias de Git para cambiar de rama sin perder cambios.**

Guarda automáticamente tus modificaciones antes de cambiar y las restaura al volver.

---

## 🚀 Instalación

Ejecuta este comando en tu terminal para añadir el alias **globalmente**:

```bash
git config --global alias.smart-switch '!f() {
  current=$(git branch --show-current);
  if ! git diff --quiet; then
    git stash push -m "autosave-$current";
  fi;
  git switch "$1";
  stash_name="autosave-$1";
  stash_id=$(git stash list | grep "$stash_name" | head -n1 | cut -d: -f1);
  if [ -n "$stash_id" ]; then
    git stash pop "$stash_id";
  fi;
}; f'
