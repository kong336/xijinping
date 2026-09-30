# xijinping

`xijinping.zip` is stored as nine GitHub-compatible binary parts because the
archive is larger than GitHub's 100 MiB per-file limit.

## Restore on Windows PowerShell

```powershell
$parts = 1..9 | ForEach-Object { "xijinping.zip.part{0:D2}" -f $_ }
$out = [System.IO.File]::Create('xijinping.zip')
try {
    foreach ($part in $parts) {
        $input = [System.IO.File]::OpenRead($part)
        try { $input.CopyTo($out) } finally { $input.Dispose() }
    }
} finally { $out.Dispose() }
```

The restored archive SHA-256 is:

`C58FD57D8EB15025D641B518B8D5575086F05B907EFB50B61669EC7D2E1421E2`
