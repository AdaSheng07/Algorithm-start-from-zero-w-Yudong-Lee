```Python3
# Python3
class Solution:
    def subdomainVisits(self, cpdomains: List[str]) -> List[str]:
        ans = collections.Counter()
        # 将cpdomains字符根据空格分解
        for segment in cpdomains:
            # 分解后得到第一个元素为count
            count = segment.split()[0]
            # 将count从string转变为int
            count = int(count)
            # 分解cpdomains后得到的第二个元素为域名segment
            segment = segment.split()[1]
            # 对域名segment根据'.'分隔后得到子域名的list
            domain = segment.split('.')
            # 对domain这个list进行遍历统计子域名次数
            for i in range(len(domain)):
                ans['.'.join(domain[i: ])] += count
        
        # 格式化输出结果
        return ["{} {}".format(count, segment) for segment, count in ans.items()]
```

