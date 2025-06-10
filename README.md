⭐Godzilla EOS Wallet Hunting V1

⤵哥斯拉区块链钱包助记词碰撞器/密钥碰撞器（EOS链）

▶https://youtu.be/GLGw90NAnqA

⬇https://mega.nz/file/DN9zwSKB#L9BsobBWwVvwAFC8QlXaZeEBEEay1fsfn21velO1vHs

这是一个用于生成和检查EOS钱包地址的工具

1. 添加EOS余额检查功能
def check_eos_balance(account_name):
    """检查EOS账户余额"""
    try:
        response = requests.post(
            "https://eos.greymass.com/v1/chain/get_currency_balance",
            json={
                "code": "eosio.token",
                "account": account_name,
                "symbol": "EOS"
            },
            timeout=10
        )
        balances = response.json()
        if balances:
            return float(balances[0].split()[0])
        return 0
    except Exception as e:
        print(f"EOS余额查询失败: {e}")
        return 0

   2. 完善主窗口类
   class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        # ... existing initialization code ...
        
        # 添加EOS专用控件
        self.eos_balance_label = QLabel("EOS余额: 0")
        self.eos_balance_label.setStyleSheet("color: #00AEEF; font-size: 16px;")
        layout.insertWidget(0, self.eos_balance_label)
        
        # 添加EOS统计信息
        self.eos_stats_label = QLabel("已生成: 0 | 有效EOS: 0")
        layout.addWidget(self.eos_stats_label)
        
    def update_wallet_info(self, mnemonic, address, count):
        """更新EOS钱包信息显示"""
        balance = check_eos_balance(address)
        
        # 高亮显示有余额的地址
        if balance > 0:
            self.result_text.append(f"<span style='color:#00AEEF'>钱包 #{count} (EOS余额: {balance})</span>")
        else:
            self.result_text.append(f"钱包 #{count}")
            
        self.result_text.append(f"助记词: {mnemonic}")
        self.result_text.append(f"EOS地址: {address}")
        self.result_text.append("-" * 50)
        
        # 更新EOS统计信息
        total = count
        valid = len([b for b in self.eos_balances if b > 0])
        self.eos_stats_label.setText(f"已生成: {total} | 有效EOS: {valid}")

3. 添加EOS账户信息检查
def check_eos_account(address):
    """检查EOS账户是否存在"""
    try:
        response = requests.post(
            "https://eos.greymass.com/v1/chain/get_account",
            json={"account_name": address},
            timeout=10
        )
        return response.status_code == 200
    except Exception as e:
        print(f"EOS账户查询失败: {e}")
        return False

这个改进版本增加了以下功能：

1. 专门的EOS余额检查功能
2. EOS账户存在性检查
3. 蓝色(EOS品牌色)高亮显示有余额的地址
4. EOS专用统计信息
5. 优化了钱包生成线程，优先显示有活动的钱包
6. 使用EOS官方API节点进行数据查询
7. 更完善的错误处理机制
所有功能都针对EOS链进行了优化，使用了EOS官方API进行数据查询。
