Trước khi vào phần này thì ta sẽ điểm sơ qua về một vài lý thuyết toán học hay, quan trọng cần dùng và khó **[ở đây](https://hackmd.io/@hlinh1908/SJ3IQWrW1x)** 



# DIFFIE-HELLMAN
## Lịch sử
**Giao thức trao đổi khóa Diffie–Hellman (DH)** là một phương pháp trao đổi khóa được phát minh sớm nhất trong mật mã học. Phương pháp trao đổi khóa **Diffie–Hellman** cho phép hai bên (người, thực thể giao tiếp) thiết lập một khóa bí mật chung để mã hóa dữ liệu sử dụng trên kênh truyền thông không an toàn mà không cần có sự thỏa thuận trước về khóa bí mật giữa hai bên. Khóa bí mật tạo ra sẽ được sử dụng để mã hóa dữ liệu với phương pháp **mã hóa khóa đối xứng** (ví dụ như **AES**)

Giao thức này được công bố đầu tiên bởi Whitfield Diffie và Martin Hellman vào năm 1976, dù rằng trước đó vài năm nó đã được phát minh một cách độc lập trong GCHQ, cơ quan tình báo Anh, bởi James H. Ellis, Clifford Cocks và Malcolm J. Williamson nhưng được giữ bí mật. Năm 2002, Hellman đề xuất thuật toán nên được gọi là trao đổi khóa Diffie–Hellman–Merkle để ghi nhận sự đóng góp của Ralph Merkle trong phát minh lĩnh vực mật mã hóa khóa công khai (Hellman, 2002).

## Thuật toán
- **Bước 1** : Chọn một số nguyên tố **lớn** $p$ để tạo nên tập các thặng dư thu gọn theo Modulo $p$ ($\mathbb{Z}^{\ast}_{p}$), và chọn ra một phần tử sinh $g$ của $\mathbb{Z}^{\ast}_{p}$. Cặp số $(p,g)$ là cặp số được hai bên Alice và Bob thỏa thuận với nhau từ trước và sẽ được gửi công khai.
- **Bước 2** : Mỗi bên Alice và Bob sẽ tự tạo cho mình **một khóa bí mật** $a$, $b$. Khóa này không nhất thiết phải là số nguyên tố, và nó hoàn toàn được bảo mật, chỉ có người sở hữu mới được biết.
- **Bước 3** : Mỗi bên sẽ tạo cho mình **một khóa công khai** (ký hiệu là $A$ và $B$) theo công thức sau :

$$
\begin{cases}
A\equiv g^a \pmod{p}\\
B\equiv g^b \pmod{p}
\end{cases}
$$

Vì đó là khóa công khai nên ai cũng sẽ biết được hai giá trị đó
- **Bước 4** : Hai bên sẽ trao đổi hai giá trị $A$ và $B$ cho nhau. Alice sẽ nhận $B$ và Bob nhận $A$ và khi đó, mỗi bên sẽ lấy giá trị mình nhận được đem đi tính phép mũ với khóa bí mật của bản thân một lần nữa như sau :

$$
\begin{cases}
s_A\equiv B^a\pmod{p}\\
s_B\equiv A^b\pmod{p}
\end{cases}
$$

$$
\Leftrightarrow
\begin{cases}
s_A\equiv (g^b)^a\pmod{p}\\
s_B\equiv (g^a)^b\pmod{p}
\end{cases}
$$

$$
\Leftrightarrow
\begin{cases}
s_A\equiv g^{ba}\pmod{p}\\
s_B\equiv g^{ab}\pmod{p}
\end{cases}
$$

$$
\Rightarrow s_A\equiv s_B\equiv g^{ab}\pmod{p}
$$

Như vậy, hai bên đã thực hiện trao đổi **khóa bí mật** $s$ thành công mà không cần phải đưa nó qua bất cứ bên thứ ba nào khác.

Lấy ví dụ : 
- Alice và Bob thỏa thuận sử dụng chung một số nguyên tố $p=23$ và phần tử sinh $g=5$
- Alice chọn một số nguyên bí mật $a=6$, và gửi cho Bob giá trị $A\equiv g^a \pmod{p}\equiv 5^6\pmod{23}\equiv 8$
- Tương tự, Bob chọn một số nguyên bí mật $b=15$, và gửi cho Alice giá trị $B\equiv g^b\pmod{p}\equiv 5^{15}\pmod{23}\equiv 19$
- Sau khi trao đổi hai giá trị công khai $A$ và $B$, Alice sẽ tính $s_A\equiv (B)^6\pmod{23}\equiv 19^6\pmod{23}\equiv 2$ và Bob cũng sẽ tính $s_B\equiv (A)^6\pmod{23}\equiv 8^{15}\pmod{23}\equiv 2$
- Như vậy, cả hai đều đã trao đổi thành công **khóa bí mật** của nhau là $s=2$.

Ta có thể minh họa quá trình trao đổi khóa kia thông qua hình vẽ sau : 
![image](https://hackmd.io/_uploads/HyHOOcfxgl.png)


Và đó là tất cả những gì mà trao đổi khóa **Diffie-Hellman** hoạt động!!!





# Discrete Logarithm Problem (DLP)
## Khái niệm 
**Discrete Logarithm Problem (DLP)**, hay bài toán logarit rời rạc là sự tiếp nối của phép tính logarit trên trường số thực vào các nhóm hữu hạn. 

Ta nhắc lại rằng : Với hai số thực $x,y$ và cơ số $a>0$, $a≠1$, nếu $a^x=y$ thì $x$ được gọi là logarit cơ số $a$ của $y$, ký hiệu $x=log_ay$.

Ta cũng định nghĩa tương tự với trường số nguyên : Cho một nhóm tuần hoàn (cyclic group) $G$ có một phần tử sinh $g$, và một phần tử $h\in G$. Tìm số mũ $x$ sao cho : 
$$
g^x=h
$$

Trong ngữ cảnh phổ biến nhất, cho nhóm nhân $\mathbb{Z}^*_p$ với $p$ là một số nguyên tố lớn, $g$ là phần tử sinh và $h\in\mathbb{Z}^*_p$. Tìm số mũ $x$ sao cho :

$$
g^x\equiv h\pmod{p}
$$

Có thể nói, đây là một bài toán khó bởi vì cho đến nay chưa ai tìm ra thuật toán chạy trong thời gian đa thức theo kích thước đầu vào (số bit của $p$) để giải DLP trong nhóm $\mathbb{Z}^*_p$

Chính vì điều đó mà DLP có tính ứng dụng cao trong mật mã học, ví dụ như : **Trao đổi khóa Diffie–Hellman**, **Mật mã ElGamal và DSA/ECDSA**,...



## Một số kỹ thuật tấn công
Tuy bài toán DLP khó là thế, song vẫn còn có một số thuật toán phức tạp, thường sinh ra từ những thuật toán tương tự cho bài toán phân tích thừa số nguyên. Chúng chạy nhanh hơn các thuật toán thô sơ, nhưng vẫn còn chậm hơn so với thời gian đa thức. Ta sẽ tìm hiểu về một số thuật toán tiêu biểu như sau :
### Baby-step Giant-step
Baby-step Giant-step là thuật toán “chuẩn” cho DLP với nhóm có độ lớn vừa phải: cho phép giảm độ phức tạp từ $O(n)$ xuống $O(\sqrt n)$. Tuy nhiên nếu như $n$ quá lớn thì thuật toán cũng trở nên khá là vô dụng.

Thuật toán : Cho $a$ là phần tử sinh của $Z_n^*$, $b$ là số nguyên dương bất kì, tính $log_a b$.
- Tính $m = \lceil \sqrt{ord(a)} \rceil = \lceil \sqrt{\phi(n)} \rceil$
- Lập bảng $(j, a^j \mod(n))$ với $0 \leq j \leq m-1$
- Lập bảng $(i, b.(a^{-m})^i) \mod(n)$ với $0 \leq i \leq m-1$
- Tra bảng tìm cặp $(i,j)$ thỏa $a^j \mod(n) = b.(a^{-m})^i \mod(n)$
- Khi đó, $log_a b = m.i + j$
>Ví dụ : Tính $log_{17} 15$ trên $Z_{97}^*$
```python= 
import math
def baby_step_giant_step(a, b, n):
    m = math.isqrt(n) + 1  
    table_j = {pow(a, j, n): j for j in range(m)}
    a_inv = pow(a, -m, n)  
    gamma = b
    
    for i in range(m):
        if gamma in table_j:  
            j = table_j[gamma]
            return i * m + j  
        gamma = (gamma * a_inv) % n  
    
    return None

a = 17  
b = 15   
n = 97      
log = baby_step_giant_step(a, b, n)
print(log)
# 31
```


### Pohlig-Hellman
**Thuật toán Pohlig–Hellman** là một thuật toán dùng để giải bài toán logarit rời rạc trong một nhóm hữu hạn, đặc biệt là khi bậc của nhóm (order) là một số có nhiều ước nguyên tố nhỏ. Thuật toán này được phát triển bởi Stephen Pohlig và Martin Hellman vào năm 1978.

Thuật toán : Tìm $x$ thỏa $g^x\equiv h\pmod{p}$. Ta có : 
- Tính $n=\phi(p)=p-1=p_1^{e_1}.p_2^{e_2}...p_k^{e_k}=\prod_{i=1}^{k} p_i$
- Đặt $x=p_i^{e_i}.q_i+r_i$, ta có : 
$$
g^x\equiv h\pmod{p}
$$

$$
\Leftrightarrow (g^x)^{\phi(p)/p_i^{e_i}}\equiv h^{\phi(p)/p_i^{e_i}}
$$

$$
\Leftrightarrow (g^{p_i^{e_i}.q_i+r_i})^{\phi(p)/p_i^{e_i}}\equiv h^{\phi(p)/p_i^{e_i}}
$$

$$
\Leftrightarrow (g^{p_i^{e_i}.q_i})^{\phi(p)/p_i^{e_i}}.(g^{r_i})^{\phi(p)/p_i^{e_i}}\equiv h^{\phi(p)/p_i^{e_i}}
$$

$$
\Leftrightarrow g^{q_i.\phi(p)}.g^{r_i.\phi(p)/p_i^{e_i}}\equiv h^{\phi(p)/p_i^{e_i}}
$$

Ta có định lý Euler như sau : Với $a<n$ và $gcd(a,n)=1$ thì : 
$$
a^{\phi(n)} \equiv 1 \pmod{n}
$$

Và vì $g<p$ và $gcd(g,p)=1$ nên ta có : 
$$
g^{q_i.\phi(p)}\equiv 1^{q_i}\pmod{p}\equiv 1\pmod{p}
$$

$$
\Leftrightarrow g^{r_i.\phi(p)/p_i^{e_i}}\equiv h^{\phi(p)/p_i^{e_i}}\pmod{p}
$$

Với các giá trị đã biết là $p_i^{e_i},\phi(p),g,h$, ta sẽ brute-force $r_i\in [0, p_i^{e_i}-1]$ sao cho nó thỏa mãn : 
$$
\Leftrightarrow g^{r_i.\phi(p)/p_i^{e_i}}\equiv h^{\phi(p)/p_i^{e_i}}\pmod{p}
$$ 

là được. Sau khi có được giá trị $r_i$ cần tìm. ta sẽ quay lại với điều kiện đặt $x$ ban đầu là : 
$$
x=p_i^{e_i}.q_i+r_i
$$

$$
\Leftrightarrow x\equiv r_i\pmod{p_i^{e_i}}
$$

Và sau khi tìm được hết tất cả giá trị $r_i$ tương ứng với từng thừa số nguyên tố $p_i^{e_i}$ của $\phi(p)$, ta sẽ lập được một hệ phương trình như sau :

$$
\begin{cases}
x \equiv r_1 \pmod{p_1^{e_1}} \\
x \equiv r_2 \pmod{p_2^{e_2}} \\
\quad \vdots \\
x \equiv r_k \pmod{p_k^{e_k}}
\end{cases}
$$

Áp dụng CRT cho hệ phương trình trên ta có : 
$$
x\pmod{\phi(p)}
$$

Như vậy, ta đã tìm được giá trị của $x$ thỏa mãn yêu cầu bài toán. 
Ảnh minh họa : ![image](https://hackmd.io/_uploads/BJmLU_Xgxl.png)


Đó chính là cách giải bài toán DLP dựa trên **thuật toán Pohlig–Hellman**. Tuy hay là thế nhưng thuật toán này cũng cần một vài điều kiện nhất định để hoạt động tốt nhất : 
- Trước hết là về vấn đề phân tích thừa số nguyên tố. Trong thực tế, Modulo $p$ (là số nguyên tố) của ta sẽ có độ dài là rất lớn ($>2048bits$). Khi đó, $\phi(p)=p-1$ cũng sẽ có độ dài tương tự với $p$. Chính vì vậy việc phân tích $\phi(p)$ thành tích các số nguyên tố nhỏ hơn sẽ mất rất nhiều thời gian, thậm chí là không thể.
- Tuy nhiên, việc phân tích có thể bị qua mặt dễ dàng nếu như $\phi(p)$ của ta là một **[Smooth Number](https://en.wikipedia.org/wiki/Smooth_number)**. Về cơ bản, Smooth number là một số nguyên dương mà tất cả các thừa số nguyên tố của nó đều nhỏ hơn hoặc bằng một giá trị nào đó. Ví dụ : $60=2^2.3.5$ là **5-smooth** vì $2,3,5\leq5$
- Vì vậy, nếu $\phi(p)$ là một **smooth number** thì việc phân tích sẽ trở nên dễ dàng và ta sẽ có được các thừa số nguyên tố để lập nên hệ phương trình như ở trên
- Những thừa số nguyên tố có được từ việc phân tích $\phi(n)$ cũng cần phải đảm bảo rằng chúng sẽ không quá lớn, bởi vì ta có bước brute-force $r_i\in [0, p_i^{e_i}-1]$. Nếu $p_i^{e_i}$ là một số lớn thì việc tìm $r_i$ sẽ mất rất nhiều thời gian, khó có thể lập được hệ phương trình Modulo.

Những điều kiện trên sẽ giúp cho thuật toán **Pohlig-Hellman** hoạt động tốt nhất có thể. Tuy nhiên, vỏ quýt dày có móng tay nhọn. Trong thực tế, việc chọn $p$ cũng đã có sự cân nhắc rất kỹ để tránh trường hợp bị tấn công bởi thuật toán này. 

Và trong số đó, ta có cách chọn $p=2q+1$, với $q$ là một số nguyên tố lớn nào đó. Tại vì sao cách chọn $p$ này lại được ưa chuộng? Bởi vì : 
- $\phi(p)=p-1=2q$ chỉ có đúng hai thừa số nguyên tố là $2$ và $q$.
- Với $2$ thì sẽ chẳng có gì đáng để nói cả, ta có thể lập được phương trình modulo đầu tiên có dạng :

$$
x\equiv r_1\pmod{2}, \hspace{4mm} r_i\in [0;2]
$$
- Còn với $q$, đây sẽ là một vấn đề vì ta có bước brute-force $r_2\in [0, q-1]$. $q$ là một số nguyên tố khác có độ dài rất là lớn. Chính vì vậy, rất khó để có thể lấy được phương trình Modulo thứ hai để tạo thành hệ phương trình Modulo để giải được.

Đó chính là cách khắc chế lại thuật toán **Pohlig-Hellman**.




### Brute-force
Tất nhiên rồi, thuật toán được yêu thích nhất của chúng ta đây =))). Cũng chẳng cần giải thích gì nhiều, cho ví dụ sau : Tìm $x$ thỏa : $3^x\equiv 13\pmod{17}$

Ta có : 
- $3^1\equiv 3\pmod{17}$
- $3^2\equiv 9\pmod{17}$
- $3^3\equiv 10\pmod{17}$
- $3^4\equiv 13\pmod{17}$

Như vậy, nghiệm của phương trình logarit rời rạc trên là $x=4$.

Code brute-force : 
```python=
g = ?
h = ?
p = ?
for x in range(1, p):
    if pow(g, x, p) == h:
        print("Nghiệm cần tìm là x =", x)
```


# Diffie-Hellman : Challenge CryptoHack
Nó có thể nằm **[ở đây](https://youtu.be/85oMrKd8afY?si=7-fEqyNfPtVcMpWP)**, hoặc **[ở đấy](https://youtu.be/Yjrfm_oRO0w?si=DqI1SGQe4PUZswIB)**.
