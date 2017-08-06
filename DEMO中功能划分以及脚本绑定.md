## <p align="center">DEMO中功能划分以及角色绑定 </p>##

 

###前言###

###引用声明###

示例依然使用**Unity酱**模型


###Player功能脚本定义 ###

- Movement
- Health
- Skill

###

###Unity酱 DEMO使用的摄像机三个定位点###


- **标准视角**
- **正面视角**
- **跳跃视角**（裙底视角→_→）

以下是三个视角的推荐配置：


**标准视角**：

- 从Unity酱资源包拉出Unity酱的模型，默认的名字是unitychan
- 新建一个空的GameObject并使之成为unitychan的子Object
- 重命名该Object的名字为：CamPos
- Position：（0，1.25，-2），Rotation：（7.5，0，0）

**正面视角**

- 新建一个空的GameObject并使之成为unitychan的子Object
- 重命名该Object的名字为：FrontPos
- Position：（0.2，1.35，2.5），Rotation：（6.25，180，0）


**跳跃视角**

- 新建一个空的GameObject并使之成为unitychan的子Object
- 重命名该Object的名字为：JumpPos
- Position：（0，0.55，-0.9），Rotation：（-45，0，0）


###第三人称视角脚本###

将该脚本代码保存为TargettoPlayer，并绑定到摄像机就可以了~
<code>

	//
	// Unity酱用第三人称，摄像机控制脚本
	// 
	// 2017/7/11
	//
	using UnityEngine;
	using System.Collections;
	
	
	public class TargettoPlayer : MonoBehaviour
	{
    public float smooth = 3f;       // 摄像机平滑系数
    Transform standardPos;          // 摄像机标准位置
    Transform frontPos;             //前置摄像机位置
    Transform jumpPos;              //跳跃摄像机位置

    // 不平滑时，快速切换标志
    bool bQuickSwitch = false;  //Change Camera Position Quickly


    void Start()
    {
        // 各个参照物的位置读取
        standardPos = GameObject.Find("CamPos").transform;

        if (GameObject.Find("FrontPos"))
            frontPos = GameObject.Find("FrontPos").transform;

        if (GameObject.Find("JumpPos"))
            jumpPos = GameObject.Find("JumpPos").transform;

        //摄像机初始位置
        transform.position = standardPos.position;
        transform.forward = standardPos.forward;
    }


    void FixedUpdate()  
    {

        if (Input.GetButton("Fire1"))   // left Ctlr
        {
            //切换前置视角
            setCameraPositionFrontView();
        }

        else if (Input.GetButton("Fire2"))  //Alt
        {
            //切换跳跃视角
            setCameraPositionJumpView();
        }

        else
        {
            //切回标准视角
            setCameraPositionNormalView();
        }
    }

    void setCameraPositionNormalView()
    {
        //快速切换标志为false，启用平滑切换
        if (bQuickSwitch == false)
        {
            //利用线性插值平滑摄像头
            transform.position = Vector3.Lerp(transform.position, standardPos.position, Time.fixedDeltaTime * smooth);
            transform.forward = Vector3.Lerp(transform.forward, standardPos.forward, Time.fixedDeltaTime * smooth);
        }
        else {
            //启用快速切换，直接赋值
            transform.position = standardPos.position;
            transform.forward = standardPos.forward;
            bQuickSwitch = false;
        }
    }


    void setCameraPositionFrontView()
    {
        // 切换前置视角，采用快速赋值方案，将QuickSwitch设为true，表示切回原来视角也使用快速方案
        bQuickSwitch = true;
        transform.position = frontPos.position;
        transform.forward = frontPos.forward;
    }

    void setCameraPositionJumpView()
    {
        //切换跳跃视角，采用平滑方案，同时将QuickSwitch设为false，表示切回原来视角也使用平滑方案
        bQuickSwitch = false;
        transform.position = Vector3.Lerp(transform.position, jumpPos.position, Time.fixedDeltaTime * smooth);
        transform.forward = Vector3.Lerp(transform.forward, jumpPos.forward, Time.fixedDeltaTime * smooth);
    }
}

</code>



### 联系方式###
个人邮箱：**suyupeng1991@gmail.com**，个人生活博客：[♂→_→♂](http://www.psy666.com)。


