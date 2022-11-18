---
{"title":"chmod command recursive","tags":"troubleshooting, programming","dg-publish":true,"permalink":"/troubleshooting/chmod-command-recursive/","dgPassFrontmatter":true}
---

## PROBLEM
chmod로 권한을 주었음에도 `permession denied`가 뜸

## REASON
chmod는 기본적으로 현재폴더 자체에만 영향을 준다. 하지만 chmod로 현재폴더에 권한을 주면 현재폴더의 하위폴더들에도 자연스럽게 권한이 부여될거라고 생각

## SOLUTION
하위폴더들에도 권한을 부여하려면 `-R` 옵션을 줘야함.

```sh
chmod 777 -R /usr
```


## [reference](https://recipes4dev.tistory.com/175)

## [reference](https://www.computerhope.com/unix/uchmod.htm)
