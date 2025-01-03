# (학습목표) 영역 자르기 ⇒ "필요한 영역만 자를 수 있나?(추출 가능한가?)"
# ※ 분석 전 차원 등 데이터 형식 확인 필요!

import netCDF4 as nc
import numpy as np
import matplotlib.pyplot as plt


# 1. *.nc 파일 열기
f_path="D:/python/0.work/20241223 ncstudy/klps_lc05_anal_20241221_0000.nc" # 파일 포맷: klps_lc05_anal_yyyyMMdd_HHmm
f_data=nc.Dataset(f_path)
f_data
f_data.variables.keys() # 변수 키 출력


# 2. 필요한 *.nc 파일 변수 읽기
lon=f_data.variables['lon'][:]
# <class 'netCDF4._netCDF4.Variable'>
# float32 lon(y, x)
#     valid_range: [-180.  180.]
#     units: degrees
#     long_name: Grid longitudes
#     _FillValue: 1e+37
# unlimited dimensions: 
# current shape = (283, 235)
# filling on

lat=f_data.variables['lat'][:]
# <class 'netCDF4._netCDF4.Variable'>
# float32 lat(y, x)
#     valid_range: [-90.  90.]
#     units: degrees
#     long_name: Grid latitudes
#     _FillValue: 1e+37
# unlimited dimensions: 
# current shape = (283, 235)
# filling on

topo=f_data.variables['staticTopo'][:]
# <class 'netCDF4._netCDF4.Variable'>
# float32 staticTopo(y, x) # (283, 235)
#     units: meters
#     long_name: Topography # 변수 설명
#     _FillValue: -99999.0 # 결측값
# unlimited dimensions: # 제한 없는 차원
# current shape = (283, 235)
# filling on


# 2-1. topo 변수 확인
print(topo)
print(topo.shape) # (283, 235)
fig, ax=plt.subplots()
qq=ax.pcolor(lon, lat, topo, cmap='terrain')
cbar=fig.colorbar(qq)
cbar.set_label('topo')


# 3. 필요한 영역 정의(≒ 남한 육지 영역)
lon_min, lon_max=124., 130.
lat_min, lat_max=33.5, 38.5

loc=np.where((lon>=lon_min)&(lon<=lon_max)&(lat>=lat_min)&(lat<=lat_max)) # 모든 조건을 충족하는 영역이어야 하므로 전체 & 처리
print(loc)
# np.where(): 인덱스만 반환 ex) a=array([5(0),6(1),7(2),8(3),9(4),10(5),11(6),12(7),13(8),14(9)]) → np.where(a>10) ⇒ (array([6,7,8,9]), )


# 4. 인덱스 슬라이싱 이용하여 영역 추출
topo_t=topo[loc[0].min():loc[0].max()+1, loc[1].min():loc[1].max()+1]
print(topo_t)
# .min(): 최소값, .max(): 최대값
# 인덱스 슬라이싱을 할 때, 끝 값을 포함하여 슬라이싱해야 하므로 .max()에 +1을 해야 함


# 4-1. 영역 추출 확인
fig, ax=plt.subplots()
qq=ax.pcolor(topo_t, cmap='terrain')
cbar=fig.colorbar(qq)
cbar.set_label('topo')
