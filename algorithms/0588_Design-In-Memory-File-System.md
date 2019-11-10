# Design In-Memory File System
------------------
@ [Description](https://leetcode.com/problems/design-in-memory-file-system/)  
@ Tags: Design    
@ Hard

------------------
## Solution
```java
class FileSystem {
    class Dir {
        public HashMap<String, Dir> dirs;
        public HashMap<String, String> files;
        public Dir() {
            dirs = new HashMap<>();
            files = new HashMap<>();
        }
    }
    
    Dir root;
    public FileSystem() {
        root = new Dir();
    }
    
    public List<String> ls(String path) {
        Dir tmp = root;
        List<String> file = new ArrayList<>();
        if (!path.equals("/")) {
            String[] d = path.split("/");
            for (int i = 1; i < d.length - 1; i++)
                tmp = tmp.dirs.get(d[i]);
            if (tmp.files.containsKey(d[d.length - 1])) {
                file.add(d[d.length - 1]);
                return file;
            } else {
                tmp = tmp.dirs.get(d[d.length - 1]);
            }
        }
        file.addAll(new ArrayList<>(tmp.dirs.keySet()));
        file.addAll(new ArrayList<>(tmp.files.keySet()));
        Collections.sort(file);
        return file;
    }
    
    public void mkdir(String path) {
        Dir tmp = root;
        String[] d = path.split("/");
        for (int i = 1; i < d.length; i++) {
            if (!tmp.dirs.containsKey(d[i]))
                tmp.dirs.put(d[i], new Dir());
            tmp = tmp.dirs.get(d[i]);
        }
    }
    
    public void addContentToFile(String filePath, String content) {
        Dir tmp = root;
        String[] d = filePath.split("/");
        for (int i = 1; i < d.length - 1; i++) {
            tmp = tmp.dirs.get(d[i]);
        }
        tmp.files.put(d[d.length - 1], tmp.files.getOrDefault(d[d.length - 1], "") + content);
    }
    
    public String readContentFromFile(String filePath) {
        Dir tmp = root;
        String[] d = filePath.split("/");
        for (int i = 1; i < d.length - 1; i++) {
            tmp = tmp.dirs.get(d[i]);
        }
        return tmp.files.get(d[d.length - 1]);
    }
}

/**
 * Your FileSystem object will be instantiated and called as such:
 * FileSystem obj = new FileSystem();
 * List<String> param_1 = obj.ls(path);
 * obj.mkdir(path);
 * obj.addContentToFile(filePath,content);
 * String param_4 = obj.readContentFromFile(filePath);
 */
 ```
