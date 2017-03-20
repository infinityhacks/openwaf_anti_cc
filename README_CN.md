Name
====

openwaf_anti_cc��[OpwnWAF](https://github.com/titansec/openwaf)��Ŀ��CC��HTTP FLOOD������ģ��

Table of Contents
=================
* [Name](#name)
* [Synopsis](#synopsis)
* [Modules Configuration Directives](#modules-configuration-directives)

Synopsis
========

[Back to TOC](#table-of-contents)

Modules Configuration Directives
================================

```txt
{
    "twaf_limit_conn": {
        "state":false,                                       -- CC����ģ�鿪��
        "log_state":true,                                    -- CC��־����
        "trigger_state":true,                                -- ��������
        "clean_state":true,                                  -- ��ϴ����
        "trigger_thr":{                                      -- ������ֵ����ϵΪ���򡱣�
            "req_flow_max":1073741824,                       -- ÿ��������������λB
            "req_count_max":10000                            -- ÿ��������
        },
        "clean_thr":{                                        -- ��ϴ��ֵ
            "new_conn_max":40,                               -- ��һԴipÿ���½�������
            "conn_max":100,                                  -- ��һԴip�����ڼ�����������
            "req_max":50,                                    -- ��һԴipÿ����������
            "uri_frequency_max":3000                         -- ��һ·��ÿ����������
        },
        "event_id":"710002",                                 -- �¼�ID
        "event_severity":"high",                             -- �¼����صȼ�
        "timer_flush_expired":10,                            -- ����shared_dict�������ݵ�ʱ����
        "interval":10,                                       -- ����CC����������־��ʱ��������λ��
        "shared_dict_name":"twaf_limit_conn",                -- ���������Ϣ��shared_dict
        "shared_dict_key": "remote_addr",                    -- shared_dict�ļ�ֵ
        "action":"DENY",                                     -- ����CC����ִ�еĶ���
        "action_meta":403,
        "timeout":30                                         -- ��ϴʱ�������ٴδ�����ϴֵʱ�����ã�
    }
}
```

###rules
**syntax:** *"state": true|false*

**default:** *false*

**context:** *twaf_limit_conn*

boolean���ͣ�CC����ģ���ܿ��أ�Ĭ�Ϲر�

###log_state
**syntax:** *"log_state": true|false*

**default:** *true*

**context:** *twaf_limit_conn*

boolean���ͣ�CC����ģ����־���أ�Ĭ�Ͽ���

###trigger_state
**syntax:** *"trigger_state": true|false*

**default:** *true*

**context:** *twaf_limit_conn*

boolean���ͣ�CC����ģ��Ĵ������أ�Ĭ�Ͽ���

���رգ��򴥷����ƹرգ�ʱ�̽���CC��ϴ״̬

###clean_state
**syntax:** *"clean_state": true|false*

**default:** *true*

**context:** *twaf_limit_conn*

boolean���ͣ�CC����ģ���ܿ��أ�Ĭ�Ͽ���

���رգ������ڲ��ԣ�������ϴ���ƹرգ�CCģ�齫�޷���������

###trigger_thr
**syntax:** *"trigger_thr": table*

**default:** *{"req_flow_max":1073741824,"req_count_max":10000}*

**context:** *twaf_limit_conn*

table���ͣ�������ֵ

���ﵽ����һ��������ֵ������CC��ϴ״̬

��ǰ������������ֵ  
```txt
    "trigger_thr":{                                      -- ������ֵ����ϵΪ���򡱣�
        "req_flow_max":1073741824,                       -- ÿ��������������λB��Ĭ��1GB/s
        "req_count_max":10000                            -- ÿ����������Ĭ��10000��/��
    }
```

###clean_thr
**syntax:** *"clean_thr": table*

**default:** *{"new_conn_max":40,"conn_max":100,"req_max":50,"uri_frequency_max":3000}*

**context:** *twaf_limit_conn*

table���ͣ���ϴ��ֵ

������CC��ϴ״̬���ﵽ����һ����ϴ��ֵ����ִ����Ӧ����

��ǰ���ĸ���ϴ��ֵ  
```txt
    "clean_thr":{                                        -- ��ϴ��ֵ����ϵΪ���򡱣�
        "new_conn_max":40,                               -- ��һԴipÿ���½���������Ĭ��40��/��
        "conn_max":100,                                  -- ��һԴip�����ڼ�������������Ĭ��100��
        "req_max":50,                                    -- ��һԴipÿ������������Ĭ��50��/��
        "uri_frequency_max":3000                         -- ��һ·��ÿ������������Ĭ��3000��/��
    }
```

###timer_flush_expired
**syntax:** *"timer_flush_expired": number*

**default:** *10*

**context:** *twaf_limit_conn*

number���ͣ�����shared_dict�������ݵ�ʱ������Ĭ��10��

###interval
**syntax:** *"interval": number*

**default:** *10*

**context:** *twaf_limit_conn*

number���ͣ�����CC����������־��ʱ������Ĭ��10��

###shared_dict_name
**syntax:** *"shared_dict_name": string*

**default:** *"twaf_limit_conn"*

**context:** *twaf_limit_conn*

string���ͣ���ŵ�ǰCC������Ϣ��shared_dict����

###shared_dict_key
**syntax:** *"shared_dict_key": string|table*

**default:** *"remote_addr"*

**context:** *twaf_limit_conn*

string��table���ͣ�shared_dict�ļ�ֵ��֧��nginx����

֧���ַ������ͺ���������
```
    "shared_dict_key": "remote_addr"
    
    "shared_dict_key": ["remote_addr", "http_user_agent"]
```

###action
**syntax:** *"action": string*

**default:** *"DENY"*

**context:** *twaf_limit_conn*

string���ͣ�����CC����ִ�еĶ�����Ĭ��"DENY"

###action_meta
**syntax:** *"action_meta": number|string*

**default:** *403*

**context:** *twaf_limit_conn*

string��number���ͣ�ִ�ж����ĸ�����Ϣ��Ĭ��403

###timeout
**syntax:** *"timeout": number*

**default:** *30*

**context:** *twaf_limit_conn*

number���ͣ���ϴʱ����N���ڲ��ٴﵽ������ֵ�����˳�CC��ϴ״̬

����ϴ�����У��ٴδﵽ������ֵ����ʱ������Ϊ30��
