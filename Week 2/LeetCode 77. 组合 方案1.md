```Java
// Java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        ans = new ArrayList<List<Integer>> ();
        set = new ArrayList<Integer> ();
        this.n = n;
        this.k = k;
        findCombo(1);
        return ans;
    }
    
    // 递归枚举1, 2,...,n每个数选/不选
    private void findCombo(int num) {
        // 当num = n + 1时，这一层递归结束，将set复制给ans
        if (num == n + 1){
            if (set.size() == k)
                ans.add(new ArrayList<Integer> (set));
            return; // 返回未执行完的上一层
        }
        // 在num不选，则看下一个元素num + 1
        findCombo(num + 1);
        // 在num选，则将num放入set中，再看下一个元素num + 1
        set.add(num);
        findCombo(num + 1);
        set.remove(set.size() - 1); // 全局变量重置，删除上一次执行的结果
    }
        
    // 四个全局变量，属于所有函数体
    private List<List<Integer>> ans;
    private List<Integer> set;
    private int n;
    private int k;

}

```
