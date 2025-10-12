import os
import sys
import platform
import subprocess

def check_environment():
    print("=== 系统信息 ===")
    print(f"操作系统: {platform.system()} {platform.release()}")
    print(f"架构: {platform.machine()}")
    print(f"Python版本: {platform.python_version()}")
    print(f"当前用户: {os.getlogin()}")
    print(f"环境变量 PATH: {os.environ.get('PATH')}")
    print()

def check_dependencies():
    print("=== 依赖库版本 ===")
    try:
        import numpy
        import scipy
        import psutil
        print(f"numpy版本: {numpy.__version__}")
        print(f"scipy版本: {scipy.__version__}")
        print(f"psutil版本: {psutil.__version__}")
    except ImportError as e:
        print(f"缺失库: {e}")
    print()

def check_hardware_access():
    print("=== 硬件/资源访问检查 ===")
    # 列出网络接口
    try:
        if platform.system() == "Windows":
            output = subprocess.check_output("netsh interface show interface", shell=True, text=True)
        else:
            output = subprocess.check_output("ip link show", shell=True, text=True)
        print("检测到网络接口:")
        print(output)
    except Exception as e:
        print(f"无法获取网络接口: {e}")
    
    # 检查CPU/GPU数量
    try:
        import psutil
        print(f"逻辑CPU核心数: {psutil.cpu_count(logical=True)}")
        print(f"物理CPU核心数: {psutil.cpu_count(logical=False)}")
    except Exception as e:
        print(f"无法获取CPU信息: {e}")

    # 检查用户权限
    try:
        print(f"是否管理员/root: {os.geteuid() == 0 if hasattr(os, 'geteuid') else '未知'}")
    except Exception as e:
        print(f"无法检查权限: {e}")

def main():
    check_environment()
    check_dependencies()
    check_hardware_access()
    print("\n=== 可用频道检测建议 ===")
    print("1. 如果网络接口为空或权限不足，工作流可能无法扫描频道。")
    print("2. 检查工作流是否允许访问底层硬件/驱动。")
    print("3. 确保工作流环境中依赖库和虚拟机一致。")

if __name__ == "__main__":
    main()
