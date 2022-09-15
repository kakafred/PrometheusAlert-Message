# PrometheusAlert-Message

## 如何使用PrometheusAlert-Message

### 1. 你可以使用以下 **git** 或者 **wget** 命令将我下载到本地电脑.
```
git https://github.com/kakafred/PrometheusAlert-Message.git

wget https://github.com/kakafred/PrometheusAlert-Message/archive/refs/heads/main.zip
```

### 2. 你可以复制模版中代码至**PrometheusAlert**消息模版.

   现只有**飞书消息**受支持. 你可以在这里查看到更多的第三方应用消息模版 > [Template Sharing Board](https://github.com/feiyu563/PrometheusAlert/issues/30)

### 3. 解释消息模版如何工作

![Lark message template v2](https://user-images.githubusercontent.com/82210954/190294297-8eb3e6dc-7386-4d7c-83d5-3c8c90ecac2d.jpeg)

**🔴 红色部分**
此部分控制着告警名称与状态的判断和输出，以实现[飞书](https://www.larksuite.com/)消息模版颜色的变更.
```shell
// 飞书代码
	var color string
	if strings.Count(text, "resolved") > 0 && strings.Count(text, "firing") > 0 {
		color = "orange"
	} else if strings.Count(text, "resolved") > 0 {
		color = "green"
	} else {
		color = "red"
	}
```
以上代码出处为[点我查看](https://github.com/feiyu563/PrometheusAlert/issues/30#issuecomment-990722433)
如果告警状态为"resolved"，则上述代码会判断并将模版颜色设置为绿色，根据代码以实现其他不同颜色的变换.
**🟡 黄色部分**
此部分控制alertmanager **Labels**标签值的接收以及输出，详细解释可参考Prometheus Label.
**🟢 绿色部分**
此部分控制alertmanager **annotations**标签值的接收以及输出，详细解释可参考Prometheus annotation.
**🔵 蓝色部分**
此部分先从url消息中将告警标签(labels)及标签值(vaules)解析，最后放入静默告警链接中.

### 4. Alertmanager-Rules 告警规则使用
将其中文件拷贝至你的prometheus目录中，并配置**prometheus.yml**文件
```shell
sudo vim /path/to/prometheus/prometheus.yml
# 加入告警文件
# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # 以文件或目录形式加载
  - "rules.yml"
  - "path/to/rules/*_rule.yml"
  # - "second_rules.yml"

# save and exit
sudo ./path/to/prometheus/promtool check config prometheus.yml
# successfully...
sudo systemctl restart prometheus
```
查看web端prometheus中Alert是否存在你所添加的告警规则

![Prometheus Alerts](https://user-images.githubusercontent.com/82210954/190299460-737f3dcd-ea6a-450c-805f-0ad4fdf92f8f.png)

## 一些些的分享链接

*🔗 Prometheus官网* > [Prometheus Web](https://prometheus.io/) 

*🔗 Prometheus官方Github* > [Prometheus](https://github.com/prometheus/prometheus) 

*🔗 PrometheusAlert全家桶Github* > [PrometheusAlert](https://github.com/feiyu563/PrometheusAlert)

*🔗 超超超级好用且通用的Prometheus告警规则*> [Alertmanager Rules](https://awesome-prometheus-alerts.grep.to/)
