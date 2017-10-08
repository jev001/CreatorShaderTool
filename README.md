# Creator Shader Tool
用于cocos creator的shader工具，支持类似于Unity3D Shader语法。

# shader语法
## 1. 概览
```
Shader "SimpleShader" {
    Properties{
        CC_Textrue0("Main Tex", texture) = "";
        _Color("Main Color", color) = (1, 1, 1, 1);
    }
    SubShader{
        Pass{
            variants = (ENABLE_COLOR, ),
            vsh = `
                attribute vec4 a_position;
                attribute vec2 a_texCoord;
                void main()
                {
                    gl_Position = CC_PMatrix * a_position;
                    v_texCoord = a_texCoord;
                }
            `;
            fsh = `
            #ifdef GL_ES
                precision mediump float;
            #endif
                varying vec2 v_texCoord;
            #if ENABLE_COLOR
                vec4 _Color;
            #endif
                void main()
                {
            #if ENABLE_COLOR
                    gl_FragColor = texture(CC_Texture0, v_texCoord) * _Color;
            #else
                    gl_FragColor = texture(CC_Texture0, v_texCoord);
            #endif
                }
            `;
        }
    }
}
```

# TODO
+ 添加材质编辑工具
