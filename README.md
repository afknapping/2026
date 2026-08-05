# 2026

Vanilla Jekyll site for GitHub Pages.

## Local dev

```
bundle install
bundle exec jekyll serve
```

If `jekyll serve`/`build` fails with `undefined method 'tainted?'`, your local Ruby is 3.2+ (which dropped `String#tainted?`/`#untaint`) — those methods were removed after `github-pages`'s pinned Jekyll/Liquid versions were written to expect them. GitHub Pages' own build servers use a Ruby version this doesn't affect, so it's a local-only issue. Workaround: load a small shim that no-ops those methods before Jekyll boots, e.g.

```
cat > /tmp/ruby4_compat_shim.rb <<'EOF'
class Object
  def tainted?; false; end
  def untaint; self; end
  def taint; self; end
end
EOF
RUBYOPT="-r/tmp/ruby4_compat_shim.rb" bundle exec jekyll serve
```

Also make sure `LANG`/`LC_ALL` are set to a UTF-8 locale (e.g. `en_US.UTF-8`) — Sass will otherwise misread non-ASCII bytes in `.css`/`.scss` files.
