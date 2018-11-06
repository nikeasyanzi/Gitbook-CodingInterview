class Solution:
    def numSubarrayProductLessThanK(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        product=1;
        j=0;
        res=0;
        if k==0:    # if k==0, the result is zero
            return 0;
        for i in range(len(nums)):
            product=product*nums[i];
            #print("product=",product);
            while product>=k and j< len(nums):  # be careful with the condition j< len(nums)
                product=product/nums[j];
                j=j+1;
            
            #print("j=",j,"i=",i,"i-j+1=",i-j+1);
            if  product<k:
                res= res+ i-j+1 ;
        #print(res);
        return res;String](/arraystring.md)

[## 560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

```python
class Solution:
    def subarraySum(self, nums, k):
        result, cur_sum = 0, 0
        sum_dict = {0:1}
        for num in nums:
            cur_sum += num    //recording the prefix sum
            if cur_sum - k in sum_dict:
                result += sum_dict[cur_sum - k]
            if cur_sum in sum_dict:
                sum_dict[cur_sum] += 1
            else:
                sum_dict[cur_sum] = 1
                
        return result
        
class Solution:
    def subarraySum(self, nums, k):

        mydict = collections.Counter()
        curr_sum=0;
        ans=0;
        for i in range(len(nums)):
            mydict[curr_sum]= mydict[curr_sum]+1;
            curr_sum=curr_sum+nums[i];
            #print (mydict);
            ans=ans+mydict[curr_sum-k];
        return ans;
```

## 說明

其實這題可以想成這樣

denote the sum between i,j as

$$
sum(i,j) = sum(0,j) - sum(0,i)
$$

$$
k = sum(0,j) - sum(0,i)
$$

所以我們可以用一個hash map 紀錄 prefix sum 出現的次數  (代表sum[0,i])

那每次疊代

* 當前的Prefix sum 次數+1
* 更新prefix sum (代表 sum[0,j])
* 更新ans by ans= ans + hash[k-prefix_sum], 


## Reference:
   * https://leetcode.com/problems/subarray-sum-equals-k/discuss/102106/Java-Solution-PreSum-%2B-HashMap
   * https://leetcode.com/problems/subarray-sum-equals-k/discuss/164431/Python-or-3-tm
   * https://zxi.mytechroad.com/blog/hashtable/leetcode-560-subarray-sum-equals-k/
    
## [930. Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum/)
這題其實也可以用560. Subarray Sum Equals K 的概念去做 
或者  帶說明


[713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/)

說明:
這題也是類似prefix的概念 外加sliding window

我們每次紀錄目前的product 與 index i

如果product > k 則開始除去前面的數 index j



```python
class Solution:
    def numSubarrayProductLessThanK(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        product=1;
        j=0;
        res=0;
        if k==0:    # if k==0, the result is zero
            return 0;
        for i in range(len(nums)):
            product=product*nums[i];
            #print("product=",product);
            while product>=k and j< len(nums):  # be careful with the condition j< len(nums)
                product=product/nums[j];
                j=j+1;

            #print("j=",j,"i=",i,"i-j+1=",i-j+1);
            if  product<k:
                res= res+ i-j+1 ;
        #print(res);
        return res;
```


##


# 类似题目：
### Two Sum

### Continuous Subarray Sum

### Subarray Product Less Than K

### Find Pivot Index