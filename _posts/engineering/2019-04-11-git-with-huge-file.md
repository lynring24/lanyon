> git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch tizen-image/*.img' --prune-empty --tag-name-filter cat -- --all
