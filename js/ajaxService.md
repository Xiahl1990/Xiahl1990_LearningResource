// Service API
function ajaxService(option){
    var _op = $.extend(true, {}, (typeof option === "object" && option));
    var isReturn = false;//是否退出后续操作
    var tuples = [
        [ "success", _op.successPreHandle, _op.successHandle ],
        [ "error", _op.errorPreHandle, _op.errorHandle ],
        [ "complete", _op.completePreHandle, _op.completeHandle ]
    ];
    var ajaxHandle = function(ajaxHandleType){
        var arg = Array.prototype.splice.call(arguments,1);
        $.each(tuples,function(i,tuple){
            if(ajaxHandleType === tuple[0]){
                // 1. 前置判断
                if($.isFunction(tuple[1])){
                    isReturn = tuple[1](arg);
                    if( isReturn ) return;
                }
                // 2. 逻辑处理
                if($.isFunction(tuple[2])){
                    isReturn = tuple[2](arg);
                    if( isReturn ) return;
                }
                // 3. 返回值
                return;
            }
        })
    }
    $.ajax({
        url: _op.url,
        type: _op.type || 'POST',
        contentType: 'application/json;charset=UTF-8',
        data: JSON.stringify(_op.data || ""),
        dataType: _op.dataType || 'json',
        async: _op.async || true,
        success:function(result, status, xhr){
            ajaxHandle("success",result, status, xhr);
        },
        error:function(xhr, status, error){
            ajaxHandle("error",xhr, status, error);
        },
        complete:function(xhr,status){
            ajaxHandle("complete",xhr, status);
        }
    })
}
