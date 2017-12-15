localProgram
```
select * from htlordermessagedb.messageplateformsendlog
where orderid in (3019491518 ) 
order by messagelogid desc;

```
```
        for (SmsMobilePhone phone : context.getMobileList()) {
            MessageBody messageBody = MessageBodyBuilder.newInstance()
                    .channel("UID", hotelOrderInfo.getUid())
                    .channel("UIDList", SmsUtils.uidList(hotelOrderInfo.getUid()))
                    .channel("EID", context.getOperator())
                    .channel("OrderID", context.getOrderId())
                    .channel("MobilePhone", phone.getPhoneNumber())
                    .channel("ScheduleTime",SmsUtils.getScheduleTime())
                    .content("SmsExpiredTime", SmsUtils.getSmsExpiredTime())
                    .content("ModuleType", phone.getModuleType())
                    .content("MsgContent", context.getRemark())
                    .build();
            SendMessageIn sendMessageIn = new SendMessageIn(context.getOperator(), messageCode, context.getOrderId(), hotelOrderInfo.getUid(), messageBody, context.getSendType());
            SendMessageOut messageOut = platformProxy.send(sendMessageIn);

            if (messageOut.isSendOK()) {
                result.add(SendResult.SmsResult.success(phone, messageCode));
            } else {
                result.add(SendResult.SmsResult.failed(phone, messageCode));
            }
        }
```
