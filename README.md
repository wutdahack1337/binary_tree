# binary_tree
binary_tree

Hôm nay, t làm bài [Cutting Woods](https://atcoder.jp/contests/abc217/tasks/abc217_d). Đọc xong đề là t biết ngay là có thể sử dụng set để giải quyết bài này. Nhưng vì quá rảnh rỗi, nên t đã tìm hiểu xem cách hoạt động đằng sau set. Sau một hồi tìm kiếm các kiểu, t biết được cây đỏ đen chính là thứ mà giúp cho set hoạt động. T quyết định tìm hiểu những gì sơ khai nhất của cây đỏ đen, đó chính là **cây nhị phân**.  
  
Lúc đầu, t code cây nhị phân bằng mảng, t cứ nghĩ chỉ cần khai báo 4*maxQ là đủ, nhưng một lúc sau t thấy đó chính là điều ngu ngốc nhất mà t có thể làm. T nhận ra rằng trong trường hợp cây thẳng hàng thì thuật toán của t sẽ chết vì nó phải chứa điều không thuộc về nó. Suy nghĩ 5' t không tìm ra giải pháp nào, t đành dùng quyền trợ giúp của google, sau đó t tìm thấy bài viết [này](https://vietcodes.github.io/algo/bst). Mặc dù hơi ngại sử dụng con trỏ và struct (vẫn ngại sau khi hoàn thành môn lập trình căn bản A), nhưng t vẫn cố gắng hiểu nó.  
```
#include <bits/stdc++.h>
#define fdto(i, a, b) for(int i = (int)a; i >= (int)b; --i)
#define fto(i, a, b) for(int i = (int)a; i <= (int)b; ++i)
using namespace std;

int n, q, c, x, mn, mx;

struct Node {
    int key;
    Node *left = nullptr, *right = nullptr;
};

Node* Insert(Node *node, int key){
    if (node == nullptr){
        node = new Node();
        node->key = key;
    } else {
        if (key < node->key){
            node->left = Insert(node->left, key);
        } else {
            node->right = Insert(node->right, key);
        }
    }

    return node;
}

void Find(Node *node, int x){
    if (node != nullptr){
        if (x < node->key){
            mx = node->key;
            Find(node->left, x);
        } else {
            mn = node->key;
            Find(node->right, x);
        }
    }
}

int main() {
    ios::sync_with_stdio(false), cin.tie(nullptr);
    cin >> n >> q;

    Node *root = nullptr;
    while (q--){
        cin >> c >> x;
        if (c == 1){
            root = Insert(root, x);
        } else {
            mn = 0, mx = n;
            Find(root, x);
            cout << mx - mn << endl;
        }
    }

    return (0-0);
}

```
  
Nhưng có một vấn đề khác vẫn còn tồn tại, mặc dù đã sử dụng con trỏ và struct để khắc phục được vấn đề bộ nhớ, nhưng t quên mất là cũng trong trường hợp cây thẳng hàng, thời gian tìm kiếm của t vẫn sẽ là O(n). Từ vấn đề đấy mới dẫn tới việc phải sử dụng cây đỏ đen (hoặc cây nhị phân cân bằng) để tối ưu về thời gian. Vì vậy, điều cần thiết là phải tìm hiểu cơ chế hoặc động của nó. Nhưng chắc có lẽ t sẽ hẹn khi khác vậy =))).  
Thế thôi ~~
