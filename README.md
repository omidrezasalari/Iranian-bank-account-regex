# check the Iranian Iban number

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
