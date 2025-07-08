当函数选择器大部分为零时，函数在 Solidity 中的效率更高。

例如

deposit278591A(uint256)具有的功能选择器，00000070 但deposit(uint256)具有的功能选择器b6b55f25

函数选择器计算为函数签名的 keccak256 的前 4 个字节。函数签名不包含变量名。例如，sendValue(uint256 amount)是错误的，但sendValue(uin256)是。

函数名的 gas 消耗是零字节数的 4 倍，非零字节数的 16 倍。因此，在最坏情况下，gas 消耗为 64 gas（4 个非零字节），在最好情况下为 28 gas（3 个零字节和 1 个非零字节）。全零的函数选择器无法编译，因为这与 fallback 函数冲突。因此，mint_22F5A30(uint256)比mint(uint256)

如果零是前导零，这将使合约更小并节省部署时的 gas。

安装 Rust
https://www.rust-lang.org/tools/install

编译
cargo build --release

运行
./target/release/eth-zero-finder "myFunctionName?(uint,address,...)" <num threads> (true|false)

问号将被替换为通过搜索找到的十六进制数字。您的函数应遵循 Solidity 函数选择器的格式。例如：无参数：“myFunction()”。一个地址参数：“myFunction(address)”。两个参数：“anotherFunction(uint256,address)”等等。

Numthreads 是要使用的线程数。最后一个 true 或 false 选项是，是否要强制将零设置为前导零。前导零可以降低部署时的 Gas 成本。

在具有 8 个线程的 MacBook Pro 上，搜索通常会在不到 30 秒的时间内找到解决方案。

示例运行：

./target/release/eth-zero-finder "withdraw_?()" 8 true
