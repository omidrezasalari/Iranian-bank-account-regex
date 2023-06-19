# 1.Iranian bank account format regex

```
Regex : /^\d+([\/.-]\d+)*$/
```

```
if(preg_match('/^\d+([\/.-]\d+)*$/', $bankAccountNumber)
{
    return true;
}

```

**Example :**

Resalat Bank : 10/6240823/1

Middle East Bank : 1007-11-040-707075053

Mellat Bank : 32.36781275



# 2. Iranian Iban number regex

```
Regex : /^[IR]{2}[0-9]{24}$/
```

```
function validateIranIban(string $shebaCode): bool
    {
        if (strlen($shebaCode) !== 26 || !preg_match('/^[IR]{2}[0-9]{24}$/', $shebaCode)) {
            return false;
        }

        $d1 = ord($shebaCode[0]) - 65 + 10;
        $d2 = ord($shebaCode[1]) - 65 + 10;

        $newStr = substr($shebaCode, 4);
        $newStr .= strval($d1) . strval($d2) . substr($shebaCode, 2, 2);

        $remainder = $this->shebaIso7064($newStr);

        return ($remainder === 1);
    }

    private function shebaIso7064($remainder): int
    {
        while (strlen($remainder) > 2) {
            $block = substr($remainder, 0, 9);
            $remainder = (intval($block, 10) % 97) . substr($remainder, strlen($block));
        }

        return intval($remainder, 10) % 97;
    }

```
