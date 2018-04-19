Others:

```c
class KthLargest {
public:
    KthLargest(int k, vector<int> nums) {
        this->k = k;
        int n = nums.size();
        for (int i = 0; i < n; ++i) {
            if (i < k) {
                q.push(nums[i]);
            } else {
                auto t = q.top();
                if (t < nums[i]) {
                    q.pop();
                    q.push(nums[i]);
                } 
            }
        }
    }
    
    int add(int val) {
        if (q.size() < k) {
            q.push(val);
        } else {
            auto t = q.top();
            if (t < val) {
                q.pop();
                q.push(val);
            }
        }
        return q.top();
    }
    
private:
    priority_queue<int, vector<int>, greater<int>> q;
    int k = 0;
};

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
```