# golang用zip打包文件简单例子

代码如下所示：

```go
package main

import (
    "archive/zip"
    "io"
    "fmt"
    "os"
)

func main() {
    files := []string{"aa", "1.txt"}
    output := "out.zip"

    newZipFile, err := os.Create(output)
    errOut(err)

    defer newZipFile.Close()

    zipWriter := zip.NewWriter(newZipFile)
    defer zipWriter.Close()

    for _, file := range files {
        fileToZip, err := os.Open(file)
        errOut(err)

        info, err := fileToZip.Stat()
        errOut(err)

        header, err := zip.FileInfoHeader(info)
        errOut(err)

        header.Name = file
        header.Method = zip.Deflate

        writer, err := zipWriter.CreateHeader(header)
        errOut(err)

        _, err = io.Copy(writer, fileToZip)
        errOut(err)
    }

    fmt.Println("zip done!")
}

func errOut(err error) {
    if err != nil {
        panic(err)
    }
}
```