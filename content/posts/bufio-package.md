+++
date = 2018-08-03T00:00:00Z
math = "true"
title = "Bufio Writer"
categories = ["bufio"]
tags = ["server"]

+++

bufio.Writer uses[]byte buffer under the hood

```
type Writer intfunc (*Writer) Write(p []byte) (n int, err error) {
    fmt.Println(len(p))
    return len(p), nil
}
func main() {
    fmt.Println("Unbuffered I/O")
    w := new(Writer)
    w.Write([]byte{'a'})
    w.Write([]byte{'b'})
    w.Write([]byte{'c'})
    w.Write([]byte{'d'})
    fmt.Println("Buffered I/O")
    bw := bufio.NewWriterSize(w, 3)
    bw.Write([]byte{'a'})
    bw.Write([]byte{'b'})
    bw.Write([]byte{'c'})
    bw.Write([]byte{'d'})
    err := bw.Flush()
    if err != nil {
        panic(err)
    }
}
Unbuffered I/O
1
1
1
1
Buffered I/O
3
1
```
