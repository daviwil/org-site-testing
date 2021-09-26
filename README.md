# Org Website Generation Experiments

I'm preparing a new series about this for [System Crafters](https://youtube.com/SystemCrafters), running some experiments here to see how reliably things work across Emacs versions.

## Conclusions

- Everything generates fine with Emacs 24.5 and up
- Installing latest Org works with Emacs 25.3 and up
- Emacs 24.1 can't install packages due to old SSL bug (my assumption)

## Ensuring Dependencies

A simple function that can be included to ensure that a package is installed.  This might not actually be necessary if you can tolerate "package already installed" messages in the script output.

```emacs-lisp
(defun ensure-package (package)
  (unless (package-installed-p package)
    (package-install package)))
```

## Ensuring Latest Org

If needed, here's how you can make sure the latest `org-mode` gets installed:

```emacs-lisp
;; Ensure latest org-mode gets installed
(assq-delete-all 'org package--builtins)
(when (boundp 'org-package--builtin-versions)
  (assq-delete-all 'org package--builtin-versions))

(package-install 'org)
```
