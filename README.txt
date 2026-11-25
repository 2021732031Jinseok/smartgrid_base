스마트그리드운용 · 데이터센터 입지 선택 실습 (필수 요구사항)
폴더 전체를 압축 해제 후 MATLAB 현재 폴더를 이 폴더로 지정한다.
R2020b 이상 권장. 기본 실행은 MATLAB 데스크톱(JVM) 사용. 최적화 툴박스 불필요.
R = explore_project1;             % 후보 모선 선택창 
R = explore_project1(25);         % 공급 가능 시간 중 총수요가 가장 큰 시점의 계통도
R = explore_project1(26,5684);    % 8월 25일 19시 (1 = 1월 1일 00시)
R = explore_project1(25,[],'solve'); % Optimization Toolbox linprog로 직접 8760시간 재계산
R.Line, R.Generator, R.Renewable, R.InfeasibleTimes
R.Flow_MW(h,k)는 시간 h의 원본 엑셀 k번째 선로 조류이다. 양수는 엑셀 from→to 방향이다.
기본 모드는 제공 엑셀로 미리 최적화한 29개 입지별 발전출력을 읽고 PTDF로 시간별 조류와 지표를 계산한다.
cache 파일은 기동·정지, 불확실성 없이 기본과제 조건만 적용한 SciPy HiGHS 결과이다.
순수 MATLAB 재계산은 선택한 모선 하나만 수행한다. 원본 파일을 재저장하면 cache 검사가 차단될 수 있다.
수요를 전부 만족하지 못하는 시간은 미공급량 대신 해 없음(NaN)으로 표시한다. 전체 연간비용과 연간 출력제한도 NaN이다.

계통도는 과제 그림의 모선 위치를 고정 사용한다. 기존 색·굵기 안내 대신 그림 아래 범례를 참고한다.
주황 90% 이상, 적색 정격 도달. 작은 화살표는 기존 부하, 자주색 이중 원은 데이터센터.
저장 예: exportgraphics(R.MapFigure,'IEEE39_bus25.png','Resolution',300)
