---
id: 5900f3ce1000cf542c50fee0
title: 'Завдання 97: великі немерсенові числа'
challengeType: 1
forumTopicId: 302214
dashedName: problem-97-large-non-mersenne-prime
---

# --description--

Перше відоме число, довжина якого становить більше мільйона цифр, знайшли в 1999 році. Це просте число Мерсенна у вигляді $2^{6972593} − 1$, яке складається з 2 098 960 цифр. Згодом виявилося, що інші числа Мерсенна у вигляді $2^p − 1$ містять ще більше цифр.

Однак у 2004 році знайшли масивне немерсенове просте число, яке складається з 2 357 207 цифр: $28433 × 2^{7830457} + 1$.

Знайдіть останні десять цифр цього числа у вигляді $multiplier × 2^{power} + 1$.

# --hints--

`largeNonMersennePrime(19, 6833086)` має повернути рядок.

```js
assert(typeof largeNonMersennePrime(19, 6833086) === 'string');
```

`largeNonMersennePrime(19, 6833086)` має повернути рядок `3637590017`.

```js
assert.strictEqual(largeNonMersennePrime(19, 6833086), '3637590017');
```

`largeNonMersennePrime(27, 7046834)` має повернути рядок `0130771969`.

```js
assert.strictEqual(largeNonMersennePrime(27, 7046834), '0130771969');
```

`largeNonMersennePrime(6679881, 6679881)` має повернути рядок `4455386113`.

```js
assert.strictEqual(largeNonMersennePrime(6679881, 6679881), '4455386113');
```

`largeNonMersennePrime(28433, 7830457)` має повернути рядок `8739992577`.

```js
assert.strictEqual(largeNonMersennePrime(28433, 7830457), '8739992577');
```

# --seed--

## --seed-contents--

```js
function largeNonMersennePrime(multiplier, power) {

  return true;
}

largeNonMersennePrime(19, 6833086);
```

# --solutions--

```js
function largeNonMersennePrime(multiplier, power) {
  function modStepsResults(number, other, mod, startValue, step) {
    let result = startValue;
    for (let i = 0; i < other; i++) {
      result = step(number, result) % mod;
    }
    return result;
  }

  const numOfDigits = 10;
  const mod = 10 ** numOfDigits;
  const digitsAfterPower = modStepsResults(2, power, mod, 1, (a, b) => a * b);
  const digitsAfterMultiply = modStepsResults(
    digitsAfterPower,
    multiplier,
    mod,
    0,
    (a, b) => a + b
  );
  const lastDigits = (digitsAfterMultiply + 1) % mod;

  return lastDigits.toString().padStart(10, '0');
}
```
