# Non-Divisible Subset
https://www.hackerrank.com/challenges/non-divisible-subset

## 思路

- 两两相加无法被 n 整除，则表示两者被 n 取余的和不为 n, 故对所有的数先对 n 取余，然后统计各个余数的个数，然后对和为n的两个余数去统计数较大的那个求和则为最终结果

## 注意的点

- 所有被 n 取余数为 0 的数，如果存在，则统计数取 1
- 如果 n 为偶数，则所有余数为 n / 2 的数，如果存在，则计数亦只取 1

## 源码(python)
```
def non_divisible_subset_count(div, data_list):
    stats_dict = dict()
    for d in data_list:
        remain = d % div
        if remain not in stats_dict:
            stats_dict[remain] = 0
        stats_dict[remain] += 1
    if 0 in stats_dict:
        stats_dict[0] = 1

    if div % 2 == 0 and div / 2 in stats_dict:
        stats_dict[div / 2] = 1
    result = 0
    key_set = set()
    for key, value in sorted([(k,v) for k,v in stats_dict.iteritems()], key=lambda x: -1 * x[1]):
        if div - key in key_set:
            continue
        result += value
        key_set.add(key)
    return result
```
