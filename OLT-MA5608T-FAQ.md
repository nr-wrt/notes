# Huawei Smart-MA5608T

## FAQ
### 1. `ont autofind` 成功, 但是 `confirm` 失败
 - ONT 产测设置的wan_mac地址(影响sn-auth的id)
 - BOB 的eeprom配置, `vendor id`是否被OLT接受
 - `display ont info` 看到

### 2. ONT Config state: failed
 - `display ont capability` 查看 omci 交互是否成功建立

 ```
 Command:
          display ont capability 0/0 0 1
  --------------------------------------------------------------------------
  ONT Hardware Capability / Status Information
  --------------------------------------------------------------------------
  F/S/P:                              0/0/0
  ONT description:                    ONT_NO_DESCRIPTION
  ONT ID:                             1
  Equipment ID:                       H2-2
  Number of uplink PON ports:         1
  Number of POTS ports:               1
  Number of ETH ports:                4
  Number of VDSL ports:               -
  Number of TDM ports:                -
  Number of MOCA ports:               -
  Number of CATV ANI ports:           -
  Number of CATV UNI ports:           -
  Number of GEM ports:                32
  IP configuration:                   support
  Number of Traffic Schedulers:       7
  Number of T-CONTs:                  8
  The type of flow control:           GEMPORT CAR and PQ
  ONT optical module power
  control capability:                 the TX and RX power can be
                                      controlled together
  ONT type:                           HGU
  Extended OMCI message format:       not support
  VoIP configuration method:          OMCI/TR069
  VoIP signalling protocol:           SIP
  ETHOAM:                             not support
  Single ring check:                  not support
  --------------------------------------------------------------------------
  Number of PQs in T-CONT   0:          -
  Number of PQs in T-CONT   1:          8
  Number of PQs in T-CONT   2:          8
  Number of PQs in T-CONT   3:          8
  Number of PQs in T-CONT   4:          8
  Number of PQs in T-CONT   5:          8
  Number of PQs in T-CONT   6:          8
  Number of PQs in T-CONT   7:          8
  --------------------------------------------------------------------------
 ```
 - 如果异常, 进 diagnose 模式, `display ont failed-configuration` 查看
   - <font size=4>__ONU GEM mapping__</font><p>
   ![alt text](asset/gem-mapping-failed.png)<br>可能原因: ONT的GEM-port下标要从0开始, 业务用mapping index表示</br>
   - <font size=4>__Get ONU capability error__</font><p>
   ![alt text](asset/omci-capability-failed.png)<br>可能原因: ONT端, omci协议报错, 检查sysinfo.xml/board.xml配置, eth网口数量, 电话口(pots)数量是  否符合硬件设计;</br>
 - 
### 3. ~