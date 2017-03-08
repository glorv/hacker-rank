# Larry's Array
https://www.hackerrank.com/challenges/larrys-array

## 思路

将题目意思简化之后，实际变为求数组中逆序对的个数

一种简单的办法是直接暴力遍历处理，则复杂度为 n^2, 一种优化的策略是，通过归并排序类似的思路，可以将复杂度降为 n*logn

## 代码
```
def get_inverted_pair_count(data_list):

    def _swap(i, j):
        tmp = data_list[i]
        data_list[i] = data_list[j]
        data_list[j] = tmp

    def merge(l, m, h):
        tmp = []
        l_index = l
        h_index = m
        cnt = 0
        while l_index < m and h_index < h:
            if data_list[l_index] <= data_list[h_index]:
                tmp.append(data_list[l_index])
                l_index += 1
            else:
                tmp.append(data_list[h_index])
                h_index += 1
                cnt += m - l_index
        if l_index < m:
            tmp.extend(data_list[l_index:m])
        else:
            tmp.extend(data_list[h_index:h])
        for i in xrange(len(tmp)):
            data_list[i+l] = tmp[i]
        return cnt

    def do_merge(l, h):
        if h - l <= 1:
            return 0
        elif h - l == 2:
            if data_list[l] < data_list[l+1]:
                return 0
            else:
                _swap(l, l+1)
                return 1
        mid = (l + h) / 2
        low_cnt = do_merge(l, mid)
        high_cnt = do_merge(mid, h)
        return low_cnt + high_cnt + merge(l, mid, h)

    return do_merge(0, len(data_list))


def larrays_array(data_list):
    return get_inverted_pair_count(data_list) % 2 == 0
```
