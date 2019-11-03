# Accounts Merge
------------------
@ [Description](https://leetcode.com/problems/accounts-merge/)  
@ Tags: DFS, Union Find     
@ Medium

------------------
## Solution 1 - Union Find
首先将每个email设为独立的set，根据account信息不断将email union在一起，最后遍历每个独立的set输出。
```java
class Solution {
    class DSU {
        int[] root;
        public DSU() {
            root = new int[10001];
            for (int i = 0; i<= 10000; i++)
                root[i] = i;
        }
        public int find(int x) {
            if (root[x] != x) root[x] = find(root[x]);
            return root[x];
        }
        public void union(int x, int y) {
            root[find(x)] = find(y);
        } 
    }
    
    
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        DSU dsu = new DSU();
        Map<String, String> emailToName = new HashMap();
        Map<String, Integer> emailToID = new HashMap();
        int id = 0;
        for (List<String> account : accounts) {
            String name = account.get(0);
            for (int i = 1; i < account.size(); i++) {
                emailToName.put(account.get(i), name);
                if (!emailToID.containsKey(account.get(i)))
                    emailToID.put(account.get(i), id++);
                dsu.union(emailToID.get(account.get(1)), emailToID.get(account.get(i)));
            }
        }
        Map<Integer, List<String>> res = new HashMap();
        for (String email : emailToName.keySet()) {
            int index = dsu.find(emailToID.get(email));
            if (res.containsKey(index)) res.get(index).add(email);
            else {
                List<String> tmp = new ArrayList<>();
                tmp.add(email);
                res.put(index, tmp);
            }
        }
        for (List<String> emails : res.values()) {
            Collections.sort(emails);
            emails.add(0, emailToName.get(emails.get(0)));
        }
        return new ArrayList(res.values());
    }
}
```

## Solution 2 - DFS
建立一个graph，将每对有关联的emails建立一个edge，用DFS遍历所有的node。  
```java
class Solution {
    public List<List<String>> accountsMerge(List<List<String>> accounts) {
        Map<String, String> emailToName = new HashMap();
        Map<String, ArrayList<String>> graph = new HashMap();
        for (List<String> account: accounts) {
            String name = "";
            for (String email: account) {
                if (name == "") {
                    name = email;
                    continue;
                }
                graph.computeIfAbsent(email, x-> new ArrayList<String>()).add(account.get(1));
                graph.computeIfAbsent(account.get(1), x-> new ArrayList<String>()).add(email);
                emailToName.put(email, name);
            }
        }

        Set<String> seen = new HashSet();
        List<List<String>> ans = new ArrayList();
        for (String email: graph.keySet()) {
            if (!seen.contains(email)) {
                seen.add(email);
                Stack<String> stack = new Stack();
                stack.push(email);
                List<String> component = new ArrayList();
                while (!stack.empty()) {
                    String node = stack.pop();
                    component.add(node);
                    for (String nei: graph.get(node)) {
                        if (!seen.contains(nei)) {
                            seen.add(nei);
                            stack.push(nei);
                        }
                    }
                }
                Collections.sort(component);
                component.add(0, emailToName.get(email));
                ans.add(component);
            }
        }
        return ans;
    }
}
```

