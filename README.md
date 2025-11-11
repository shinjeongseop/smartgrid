<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SmartGrid API 문서</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css">
  <style>
    body { padding: 20px; background: #f8f9fa; }
    .container { max-width: 1400px; background: white; padding: 30px; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
    h1 { color: #0d6efd; margin-bottom: 30px; }
    h2 { color: #495057; margin-top: 40px; margin-bottom: 20px; border-bottom: 2px solid #0d6efd; padding-bottom: 10px; }
    .table { font-size: 14px; }
    .table thead { background: #0d6efd; color: white; }
    .badge { font-size: 11px; }
    code { background: #f1f3f5; padding: 2px 6px; border-radius: 3px; color: #d63384; }
    .nav-tabs { margin-bottom: 20px; }
    .example-code { background: #f8f9fa; padding: 15px; border-radius: 5px; border-left: 4px solid #0d6efd; margin: 10px 0; }
    .type-badge { font-weight: 600; }
  </style>
</head>
<body>
  <div class="container">
    <h1><i class="bi bi-table"></i> SmartGrid API 문서</h1>
    <p class="lead">강력한 데이터 그리드 라이브러리 - 클라이언트/서버 페이징, 정렬, 편집, 엑셀 연동 지원</p>

    <!-- 목차 -->
    <ul class="nav nav-tabs" role="tablist">
      <li class="nav-item">
        <a class="nav-link active" data-bs-toggle="tab" href="#columns">컬럼 정의</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" data-bs-toggle="tab" href="#options">그리드 옵션</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" data-bs-toggle="tab" href="#methods">메서드</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" data-bs-toggle="tab" href="#events">이벤트</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" data-bs-toggle="tab" href="#plugins">플러그인</a>
      </li>
    </ul>

    <div class="tab-content">
      <!-- 컬럼 정의 -->
      <div id="columns" class="tab-pane fade show active">
        <h2>컬럼 정의 (columns)</h2>
        
        <h4 class="mt-4">기본 속성</h4>
        <table class="table table-bordered table-striped table-hover">
          <thead>
            <tr>
              <th style="width: 150px;">속성명</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>field</code></td>
              <td><span class="badge bg-danger type-badge">String</span></td>
              <td><span class="badge bg-warning text-dark">필수</span></td>
              <td>데이터 필드명 (고유 식별자)</td>
            </tr>
            <tr>
              <td><code>title</code></td>
              <td><span class="badge bg-danger type-badge">String</span></td>
              <td><code>field</code> 값</td>
              <td>컬럼 헤더 표시명</td>
            </tr>
            <tr>
              <td><code>width</code></td>
              <td><span class="badge bg-danger type-badge">String</span></td>
              <td><code>'auto'</code></td>
              <td>컬럼 너비 (예: '120px', '10%')</td>
            </tr>
            <tr>
              <td><code>headAlign</code></td>
              <td><span class="badge bg-danger type-badge">String</span></td>
              <td><code>'center'</code></td>
              <td>헤더 정렬 (left/center/right)</td>
            </tr>
            <tr>
              <td><code>cellAlign</code></td>
              <td><span class="badge bg-danger type-badge">String</span></td>
              <td><code>'left'</code></td>
              <td>셀 정렬 (numberbox는 'right')</td>
            </tr>
            <tr>
              <td><code>sortable</code></td>
              <td><span class="badge bg-primary type-badge">Boolean</span></td>
              <td><code>false</code></td>
              <td>정렬 가능 여부</td>
            </tr>
            <tr>
              <td><code>hideColumn</code></td>
              <td><span class="badge bg-primary type-badge">Boolean</span></td>
              <td><code>false</code></td>
              <td>컬럼 숨김 여부</td>
            </tr>
            <tr>
              <td><code>sum</code></td>
              <td><span class="badge bg-primary type-badge">Boolean</span></td>
              <td><code>false</code></td>
              <td>푸터에 합계 표시 (numberbox만)</td>
            </tr>
            <tr>
              <td><code>formula</code></td>
              <td><span class="badge bg-success type-badge">Function</span></td>
              <td><code>null</code></td>
              <td>계산식 함수 <code>(row, col, idx) => value</code></td>
            </tr>
            <tr>
              <td><code>render</code></td>
              <td><span class="badge bg-success type-badge">Function</span></td>
              <td><code>null</code></td>
              <td>커스텀 렌더링 <code>(val, row, col) => html</code></td>
            </tr>
            <tr>
              <td><code>editor</code></td>
              <td><span class="badge bg-info type-badge">Object</span></td>
              <td><code>{type: 'textbox'}</code></td>
              <td>에디터 설정 (아래 표 참조)</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">에디터 타입별 설정 (editor)</h4>
        
        <h5 class="mt-4"><i class="bi bi-input-cursor-text"></i> textbox (기본 텍스트)</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 150px;">속성</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr><td><code>type</code></td><td><span class="badge bg-danger">String</span></td><td><code>'textbox'</code></td><td>에디터 타입</td></tr>
            <tr><td><code>placeholder</code></td><td><span class="badge bg-danger">String</span></td><td><code>''</code></td><td>입력 힌트</td></tr>
            <tr><td><code>required</code></td><td><span class="badge bg-primary">Boolean</span></td><td><code>false</code></td><td>필수 입력</td></tr>
            <tr><td><code>readonly</code></td><td><span class="badge bg-primary">Boolean</span></td><td><code>false</code></td><td>읽기 전용</td></tr>
            <tr><td><code>editable</code></td><td><span class="badge bg-primary">Boolean</span></td><td><code>true</code></td><td>편집 가능</td></tr>
            <tr><td><code>defaultVal</code></td><td><span class="badge bg-secondary">Any</span></td><td><code>''</code></td><td>기본값 또는 함수</td></tr>
            <tr><td><code>validate</code></td><td><span class="badge bg-success">Function</span></td><td><code>null</code></td><td>유효성 검사 <code>(val, row, col) => true | string</code></td></tr>
          </tbody>
        </table>

        <h5 class="mt-4"><i class="bi bi-123"></i> numberbox (숫자)</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 150px;">속성</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr><td><code>type</code></td><td><span class="badge bg-danger">String</span></td><td><code>'numberbox'</code></td><td>에디터 타입</td></tr>
            <tr><td><code>decimalPlaces</code></td><td><span class="badge bg-warning">Number</span></td><td><code>0</code></td><td>소수점 자릿수</td></tr>
            <tr><td><code>min</code></td><td><span class="badge bg-warning">Number</span></td><td><code>undefined</code></td><td>최소값</td></tr>
            <tr><td><code>max</code></td><td><span class="badge bg-warning">Number</span></td><td><code>undefined</code></td><td>최대값</td></tr>
            <tr><td><code>step</code></td><td><span class="badge bg-warning">Number</span></td><td><code>'any'</code></td><td>증감 단위</td></tr>
            <tr><td><code>defaultVal</code></td><td><span class="badge bg-warning">Number</span></td><td><code>0</code></td><td>기본값</td></tr>
            <tr><td><code>required</code></td><td><span class="badge bg-primary">Boolean</span></td><td><code>false</code></td><td>필수 입력</td></tr>
          </tbody>
        </table>

        <h5 class="mt-4"><i class="bi bi-calendar3"></i> datebox (날짜)</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 150px;">속성</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr><td><code>type</code></td><td><span class="badge bg-danger">String</span></td><td><code>'datebox'</code></td><td>에디터 타입</td></tr>
            <tr><td><code>defaultVal</code></td><td><span class="badge bg-secondary">Any</span></td><td><code>''</code></td><td>기본값 (함수 가능)</td></tr>
            <tr><td><code>required</code></td><td><span class="badge bg-primary">Boolean</span></td><td><code>false</code></td><td>필수 입력</td></tr>
          </tbody>
        </table>

        <h5 class="mt-4"><i class="bi bi-menu-button-wide"></i> selectbox (드롭다운)</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 150px;">속성</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr><td><code>type</code></td><td><span class="badge bg-danger">String</span></td><td><code>'selectbox'</code></td><td>에디터 타입</td></tr>
            <tr><td><code>options</code></td><td><span class="badge bg-info">Array</span></td><td><code>[]</code></td><td>정적 옵션 배열</td></tr>
            <tr><td><code>url</code></td><td><span class="badge bg-danger">String</span></td><td><code>null</code></td><td>동적 로딩 URL (JSON 배열 반환)</td></tr>
            <tr><td><code>valueField</code></td><td><span class="badge bg-danger">String</span></td><td><code>'value'</code></td><td>값 필드명</td></tr>
            <tr><td><code>textField</code></td><td><span class="badge bg-danger">String</span></td><td><code>'text'</code></td><td>표시 필드명</td></tr>
            <tr><td><code>defaultVal</code></td><td><span class="badge bg-secondary">Any</span></td><td>첫 번째 옵션</td><td>기본값</td></tr>
            <tr><td><code>required</code></td><td><span class="badge bg-primary">Boolean</span></td><td><code>false</code></td><td>필수 선택</td></tr>
          </tbody>
        </table>

        <h5 class="mt-4"><i class="bi bi-check-square"></i> checkbox (체크박스)</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 150px;">속성</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr><td><code>type</code></td><td><span class="badge bg-danger">String</span></td><td><code>'checkbox'</code></td><td>에디터 타입</td></tr>
            <tr><td><code>defaultVal</code></td><td><span class="badge bg-primary">Boolean</span></td><td><code>false</code></td><td>기본 체크 상태 (true/false, 1/0)</td></tr>
          </tbody>
        </table>

        <h5 class="mt-4"><i class="bi bi-ui-radios"></i> radiobutton (라디오)</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 150px;">속성</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr><td><code>type</code></td><td><span class="badge bg-danger">String</span></td><td><code>'radiobutton'</code></td><td>에디터 타입</td></tr>
            <tr><td><code>options</code></td><td><span class="badge bg-info">Array</span></td><td><code>[]</code></td><td>옵션 배열 (val, text)</td></tr>
            <tr><td><code>defaultVal</code></td><td><span class="badge bg-secondary">Any</span></td><td>첫 번째 옵션</td><td>기본값</td></tr>
          </tbody>
        </table>

        <h5 class="mt-4"><i class="bi bi-textarea-t"></i> textarea (텍스트 영역)</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 150px;">속성</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 120px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr><td><code>type</code></td><td><span class="badge bg-danger">String</span></td><td><code>'textarea'</code></td><td>에디터 타입</td></tr>
            <tr><td><code>placeholder</code></td><td><span class="badge bg-danger">String</span></td><td><code>''</code></td><td>입력 힌트</td></tr>
            <tr><td><code>defaultVal</code></td><td><span class="badge bg-danger">String</span></td><td><code>''</code></td><td>기본값</td></tr>
          </tbody>
        </table>

        <h5 class="mt-4"><i class="bi bi-three-dots"></i> 기타 HTML5 타입</h5>
        <div class="alert alert-info">
          <strong>지원 타입:</strong> <code>email</code>, <code>password</code>, <code>tel</code>, <code>url</code>, 
          <code>datetime-local</code>, <code>month</code>, <code>week</code>, <code>time</code>, 
          <code>color</code>, <code>range</code>
        </div>
      </div>

      <!-- 그리드 옵션 -->
      <div id="options" class="tab-pane fade">
        <h2>그리드 옵션 (options)</h2>
        
        <h4 class="mt-4">데이터 관련</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 180px;">옵션명</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 150px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>idField</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>'id'</code></td>
              <td>행 고유 식별자 필드명</td>
            </tr>
            <tr>
              <td><code>columns</code></td>
              <td><span class="badge bg-info">Array</span></td>
              <td><code>[]</code></td>
              <td>컬럼 정의 배열</td>
            </tr>
            <tr>
              <td><code>pageSize</code></td>
              <td><span class="badge bg-warning">Number</span></td>
              <td><code>10</code></td>
              <td>페이지당 행 수</td>
            </tr>
            <tr>
              <td><code>page</code></td>
              <td><span class="badge bg-warning">Number</span></td>
              <td><code>1</code></td>
              <td>초기 페이지 번호</td>
            </tr>
            <tr>
              <td><code>pagingMode</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>'client'</code></td>
              <td>페이징 모드 ('client' | 'server')</td>
            </tr>
            <tr>
              <td><code>loadFilter</code></td>
              <td><span class="badge bg-success">Function</span></td>
              <td><code>null</code></td>
              <td>데이터 로드 전 전처리 함수</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">서버 모드 설정 (pagingMode: 'server')</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 180px;">옵션명</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 150px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>url</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>null</code></td>
              <td>데이터 조회 URL (필수)</td>
            </tr>
            <tr>
              <td><code>writeUrl</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>null</code></td>
              <td>데이터 추가 URL</td>
            </tr>
            <tr>
              <td><code>updateUrl</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>null</code></td>
              <td>데이터 수정 URL</td>
            </tr>
            <tr>
              <td><code>deleteUrl</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>null</code></td>
              <td>데이터 삭제 URL</td>
            </tr>
            <tr>
              <td><code>queryParams</code></td>
              <td><span class="badge bg-info">Object</span></td>
              <td><code>{}</code></td>
              <td>기본 쿼리 파라미터</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">UI 설정</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 180px;">옵션명</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 150px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>width</code></td>
              <td><span class="badge bg-danger">String/Number</span></td>
              <td><code>undefined</code></td>
              <td>그리드 너비</td>
            </tr>
            <tr>
              <td><code>height</code></td>
              <td><span class="badge bg-danger">String/Number</span></td>
              <td><code>undefined</code></td>
              <td>그리드 높이</td>
            </tr>
            <tr>
              <td><code>rowHeight</code></td>
              <td><span class="badge bg-warning">Number</span></td>
              <td><code>35</code></td>
              <td>행 높이 (px)</td>
            </tr>
            <tr>
              <td><code>enableCheckboxColumn</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>true</code></td>
              <td>체크박스 컬럼 표시</td>
            </tr>
            <tr>
              <td><code>enableIndexColumn</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>true</code></td>
              <td>번호 컬럼 표시</td>
            </tr>
            <tr>
              <td><code>enableToolbar</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>true</code></td>
              <td>툴바 표시</td>
            </tr>
            <tr>
              <td><code>enablePagination</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>true</code></td>
              <td>페이징 표시</td>
            </tr>
            <tr>
              <td><code>enableTotalRows</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>true</code></td>
              <td>전체 행 수 표시</td>
            </tr>
            <tr>
              <td><code>enablePageSizeSelect</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>true</code></td>
              <td>페이지 크기 선택 표시</td>
            </tr>
            <tr>
              <td><code>enableEditMode</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>true</code></td>
              <td>편집 모드 활성화</td>
            </tr>
            <tr>
              <td><code>isEditMode</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>false</code></td>
              <td>초기 편집 모드 여부</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">툴바 버튼 설정</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 180px;">옵션명</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 200px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>toolbarButtons</code></td>
              <td><span class="badge bg-info">Array</span></td>
              <td><code>['Add', 'Edit', 'Save', 'Cancel', 'Delete', 'Print']</code></td>
              <td>표시할 버튼 목록</td>
            </tr>
          </tbody>
        </table>
        <div class="alert alert-secondary mt-2">
          <strong>사용 가능한 버튼:</strong> Add, Edit, Save, Cancel, Delete, Print
        </div>

        <h4 class="mt-5">이벤트 콜백</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 180px;">옵션명</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 150px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>onLoadSuccess</code></td>
              <td><span class="badge bg-success">Function</span></td>
              <td><code>null</code></td>
              <td>데이터 로드 성공 시 <code>(data, total, grid) => {}</code></td>
            </tr>
            <tr>
              <td><code>onLoadError</code></td>
              <td><span class="badge bg-success">Function</span></td>
              <td><code>null</code></td>
              <td>데이터 로드 실패 시 <code>(error, grid) => {}</code></td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">디버그</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 180px;">옵션명</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 150px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>debug</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>false</code></td>
              <td>디버그 모드 활성화</td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- 메서드 -->
      <div id="methods" class="tab-pane fade">
        <h2>메서드</h2>
        
        <h4 class="mt-4">데이터 로드/조회</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>loadData(data)</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>클라이언트 모드에서 배열 데이터 로드</td>
            </tr>
            <tr>
              <td><code>fetchData(params)</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>서버 모드에서 데이터 조회 (파라미터 객체 전달)</td>
            </tr>
            <tr>
              <td><code>getData()</code></td>
              <td><span class="badge bg-info">Array</span></td>
              <td>정렬된 전체 데이터 반환</td>
            </tr>
            <tr>
              <td><code>getRows()</code></td>
              <td><span class="badge bg-info">Array</span></td>
              <td>현재 페이지 데이터 반환</td>
            </tr>
            <tr>
              <td><code>getCheckedRows()</code></td>
              <td><span class="badge bg-info">Array</span></td>
              <td>체크된 행 데이터 반환</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">CRUD 작업</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>addRow()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>새 행 추가 (첫 행에 삽입)</td>
            </tr>
            <tr>
              <td><code>saveRow()</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>변경사항 저장 (서버 모드: API 호출)</td>
            </tr>
            <tr>
              <td><code>deleteRow()</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>체크된 행 삭제</td>
            </tr>
            <tr>
              <td><code>rejectRow()</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>변경사항 취소 (원본 복원)</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">편집 모드</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>setEditMode(enabled)</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>편집 모드 활성화/비활성화 (true/false)</td>
            </tr>
            <tr>
              <td><code>getEditMode()</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>현재 편집 모드 상태 반환</td>
            </tr>
            <tr>
              <td><code>isEditModeEnabled()</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>편집 모드 기능 활성화 여부 반환</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">페이징/정렬</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>setPageSize(size)</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>페이지 크기 설정</td>
            </tr>
            <tr>
              <td><code>changePage()</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>페이지 변경 적용 (currentPage 기준)</td>
            </tr>
            <tr>
              <td><code>sortColumn(field)</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>컬럼 정렬 (asc → desc → 해제)</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">컬럼 제어</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>hideColumn(field)</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>컬럼 숨김</td>
            </tr>
            <tr>
              <td><code>showColumn(field)</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>숨긴 컬럼 표시</td>
            </tr>
            <tr>
              <td><code>setRowHeight(height, reRender)</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>행 높이 설정 (px 단위, reRender 기본값: true)</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">렌더링</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>renderGrid()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>그리드 전체 재렌더링</td>
            </tr>
            <tr>
              <td><code>renderPagination()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>페이징 UI 재렌더링</td>
            </tr>
            <tr>
              <td><code>updateTotalRowsInfo()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>전체 행 수 정보 업데이트</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">UI 컴포넌트</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>showLoading()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>로딩 스피너 표시</td>
            </tr>
            <tr>
              <td><code>hideLoading()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>로딩 스피너 숨김</td>
            </tr>
            <tr>
              <td><code>showToast(msg, type)</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>토스트 메시지 표시 (type: info/success/error/warning)</td>
            </tr>
            <tr>
              <td><code>showConfirmModal(msg, callback)</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>확인 모달 표시 (callback: (confirmed) => {})</td>
            </tr>
            <tr>
              <td><code>printCurrentPage()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>현재 페이지 인쇄 미리보기</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">플러그인</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>use(Plugin, options)</code></td>
              <td><span class="badge bg-info">SmartGrid</span></td>
              <td>플러그인 등록 (체이닝 가능)</td>
            </tr>
            <tr>
              <td><code>removePlugin(name)</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>플러그인 제거</td>
            </tr>
            <tr>
              <td><code>hasPlugin(name)</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>플러그인 존재 여부 확인</td>
            </tr>
            <tr>
              <td><code>getPlugin(name)</code></td>
              <td><span class="badge bg-info">Object|null</span></td>
              <td>플러그인 인스턴스 반환</td>
            </tr>
            <tr>
              <td><code>getPluginNames()</code></td>
              <td><span class="badge bg-info">Array</span></td>
              <td>등록된 플러그인 이름 목록</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">이벤트</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>on(eventName, listener)</code></td>
              <td><span class="badge bg-success">Function</span></td>
              <td>이벤트 리스너 등록 (제거 함수 반환)</td>
            </tr>
            <tr>
              <td><code>once(eventName, listener)</code></td>
              <td><span class="badge bg-success">Function</span></td>
              <td>일회성 이벤트 리스너 등록</td>
            </tr>
            <tr>
              <td><code>off(eventName, listener)</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>이벤트 리스너 제거</td>
            </tr>
            <tr>
              <td><code>emit(eventName, ...args)</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>이벤트 발생</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">유틸리티</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>validateChanges()</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td>변경 데이터 유효성 검사</td>
            </tr>
            <tr>
              <td><code>findRowData(rowId)</code></td>
              <td><span class="badge bg-info">Object|null</span></td>
              <td>행 ID로 데이터 조회</td>
            </tr>
            <tr>
              <td><code>destroy()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>그리드 인스턴스 파괴 (메모리 정리)</td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">정적 메서드</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 250px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>SmartGrid.getInstance(id)</code></td>
              <td><span class="badge bg-info">SmartGrid|null</span></td>
              <td>인스턴스 ID로 그리드 조회</td>
            </tr>
            <tr>
              <td><code>SmartGrid.findByTableId(tableId)</code></td>
              <td><span class="badge bg-info">SmartGrid|null</span></td>
              <td>테이블 ID로 그리드 조회</td>
            </tr>
            <tr>
              <td><code>SmartGrid.getAllInstances()</code></td>
              <td><span class="badge bg-info">Array</span></td>
              <td>모든 그리드 인스턴스 반환</td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- 이벤트 -->
      <div id="events" class="tab-pane fade">
        <h2>이벤트</h2>
        
        <h4 class="mt-4">데이터 로드</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 200px;">이벤트명</th>
              <th style="width: 150px;">타이밍</th>
              <th>파라미터</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>beforeLoad</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ params, cancelled }</code><br><small>cancelled를 true로 설정 시 로드 취소</small></td>
            </tr>
            <tr>
              <td><code>afterLoad</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ data, totalRows }</code></td>
            </tr>
            <tr>
              <td><code>loadError</code></td>
              <td><span class="badge bg-danger">오류</span></td>
              <td><code>{ error }</code></td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">페이지/정렬</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 200px;">이벤트명</th>
              <th style="width: 150px;">타이밍</th>
              <th>파라미터</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>beforePageChange</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ currentPage, cancelled }</code></td>
            </tr>
            <tr>
              <td><code>afterPageChange</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ currentPage }</code></td>
            </tr>
            <tr>
              <td><code>beforeSort</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ field, sortOrders }</code></td>
            </tr>
            <tr>
              <td><code>afterSort</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ field, sortOrders }</code></td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">행 편집</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 200px;">이벤트명</th>
              <th style="width: 150px;">타이밍</th>
              <th>파라미터</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>beforeRowAdd</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ cancelled }</code></td>
            </tr>
            <tr>
              <td><code>afterRowAdd</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ row }</code></td>
            </tr>
            <tr>
              <td><code>beforeRowDelete</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ rows, cancelled }</code></td>
            </tr>
            <tr>
              <td><code>afterRowDelete</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ rows }</code></td>
            </tr>
            <tr>
              <td><code>beforeCellChange</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ rowData, field, oldValue, newValue, cancelled }</code></td>
            </tr>
            <tr>
              <td><code>afterCellChange</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ rowData, field, oldValue, newValue }</code></td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">저장/취소</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 200px;">이벤트명</th>
              <th style="width: 150px;">타이밍</th>
              <th>파라미터</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>beforeSave</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ changes, cancelled }</code><br><small>changes: { newRows, updatedRows, deletedRows }</small></td>
            </tr>
            <tr>
              <td><code>afterSave</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ changes }</code> 또는 <code>{ results }</code> (서버 모드)</td>
            </tr>
            <tr>
              <td><code>saveError</code></td>
              <td><span class="badge bg-danger">오류</span></td>
              <td><code>{ error, changes }</code></td>
            </tr>
            <tr>
              <td><code>beforeCancel</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ changes, cancelled }</code></td>
            </tr>
            <tr>
              <td><code>afterCancel</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{}</code></td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">편집 모드</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 200px;">이벤트명</th>
              <th style="width: 150px;">타이밍</th>
              <th>파라미터</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>beforeEditModeChange</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ previousMode, newMode, cancelled }</code></td>
            </tr>
            <tr>
              <td><code>afterEditModeChange</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ previousMode, currentMode }</code></td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">유효성 검사</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 200px;">이벤트명</th>
              <th style="width: 150px;">타이밍</th>
              <th>파라미터</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>beforeValidate</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{ rowsToValidate, cancelled }</code></td>
            </tr>
            <tr>
              <td><code>afterValidate</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ isValid, errors }</code></td>
            </tr>
            <tr>
              <td><code>validationError</code></td>
              <td><span class="badge bg-danger">오류</span></td>
              <td><code>{ rowData, column, value, message }</code></td>
            </tr>
          </tbody>
        </table>

        <h4 class="mt-5">기타</h4>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 200px;">이벤트명</th>
              <th style="width: 150px;">타이밍</th>
              <th>파라미터</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>error</code></td>
              <td><span class="badge bg-danger">오류</span></td>
              <td><code>{ message, code, context, instanceId, timestamp, stack }</code></td>
            </tr>
            <tr>
              <td><code>warning</code></td>
              <td><span class="badge bg-warning">경고</span></td>
              <td><code>{ code, message, details, instanceId, timestamp }</code></td>
            </tr>
            <tr>
              <td><code>beforeDestroy</code></td>
              <td><span class="badge bg-warning">사전</span></td>
              <td><code>{}</code></td>
            </tr>
            <tr>
              <td><code>pluginRegistered</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ name, version, instance }</code></td>
            </tr>
            <tr>
              <td><code>pluginUnregistered</code></td>
              <td><span class="badge bg-success">사후</span></td>
              <td><code>{ name }</code></td>
            </tr>
          </tbody>
        </table>

        <div class="example-code mt-4">
          <h5>이벤트 사용 예제</h5>
          <pre><code>// 이벤트 리스너 등록
grid.on('afterLoad', ({ data, totalRows }) => {
  console.log(`${totalRows}건의 데이터가 로드되었습니다.`);
});

// 저장 전 검증
grid.on('beforeSave', ({ changes, cancelled }) => {
  if (changes.newRows.length === 0) {
    grid.showToast('저장할 데이터가 없습니다.', 'warning');
    cancelled = true; // 저장 취소
  }
});

// 셀 변경 시 다른 셀 자동 업데이트
grid.on('afterCellChange', ({ rowData, field }) => {
  if (field === 'quantity' || field === 'price') {
    rowData.total = rowData.quantity * rowData.price;
    grid.renderGrid();
  }
});</code></pre>
        </div>
      </div>

      <!-- 플러그인 -->
      <div id="plugins" class="tab-pane fade">
        <h2>플러그인</h2>
        
        <h3 class="mt-4"><i class="bi bi-file-earmark-excel"></i> Excel 플러그인 (GridExcelPlugin)</h3>
        
        <h5 class="mt-4">설치</h5>
        <div class="example-code">
          <pre><code>grid.use(GridExcelPlugin, {
  columnMap: { '엑셀헤더': 'fieldName' },  // 선택사항 (자동 생성)
  validationRules: {                       // 선택사항 (자동 생성)
    '엑셀헤더': { required: true }
  },
  dataProcessor: (data) => data            // 전처리 함수 (선택)
});</code></pre>
        </div>

        <h5 class="mt-4">메서드</h5>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 280px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>excel.upload(file, options)</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>엑셀 파일 업로드 및 처리</td>
            </tr>
            <tr>
              <td><code>excel.download(fileName)</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>그리드 데이터를 엑셀로 다운로드</td>
            </tr>
            <tr>
              <td><code>excel.send(options)</code></td>
              <td><span class="badge bg-info">Promise</span></td>
              <td>그리드 데이터를 서버로 전송</td>
            </tr>
          </tbody>
        </table>

        <h5 class="mt-4">upload 옵션</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 180px;">옵션</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 150px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>mode</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>'preview'</code></td>
              <td>'preview' (그리드 표시) | 'direct' (서버 전송)</td>
            </tr>
            <tr>
              <td><code>url</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>null</code></td>
              <td>direct 모드 시 서버 URL</td>
            </tr>
            <tr>
              <td><code>columnMap</code></td>
              <td><span class="badge bg-info">Object</span></td>
              <td>자동 생성</td>
              <td>엑셀 헤더 → 필드명 매핑</td>
            </tr>
            <tr>
              <td><code>validationRules</code></td>
              <td><span class="badge bg-info">Object</span></td>
              <td>자동 생성</td>
              <td>유효성 검사 규칙</td>
            </tr>
            <tr>
              <td><code>dataProcessor</code></td>
              <td><span class="badge bg-success">Function</span></td>
              <td><code>null</code></td>
              <td>데이터 전처리 함수</td>
            </tr>
            <tr>
              <td><code>clearAfterSend</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>false</code></td>
              <td>전송 후 그리드 초기화 여부</td>
            </tr>
            <tr>
              <td><code>skipConfirm</code></td>
              <td><span class="badge bg-primary">Boolean</span></td>
              <td><code>false</code></td>
              <td>확인 모달 건너뛰기 (send 메서드)</td>
            </tr>
          </tbody>
        </table>

        <h5 class="mt-4">사용 예제</h5>
        <div class="example-code">
          <pre><code>// 1. 엑셀 업로드 (미리보기 모드)
await grid.excel.upload(file, {
  mode: 'preview',
  dataProcessor: (data) => {
    // 데이터 전처리
    return data.map(row => ({
      ...row,
      status: row.status || 'pending'
    }));
  }
});

// 2. 엑셀 업로드 (직접 전송 모드)
await grid.excel.upload(file, {
  mode: 'direct',
  url: '/api/bulk-upload',
  columnMap: {
    '상품명': 'productName',
    '수량': 'quantity',
    '가격': 'price'
  }
});

// 3. 엑셀 다운로드
await grid.excel.download('재고현황_' + new Date().toISOString().split('T')[0] + '.xlsx');

// 4. 그리드 데이터 서버 전송
await grid.excel.send({
  url: '/api/save-data',
  skipConfirm: false
});</code></pre>
        </div>

        <h3 class="mt-5"><i class="bi bi-bar-chart-fill"></i> Chart 플러그인 (GridChartPlugin)</h3>
        
        <h5 class="mt-4">설치</h5>
        <div class="example-code">
          <pre><code>grid.use(GridChartPlugin, {
  defaultChartType: 'bar',      // 기본 차트 타입
  modalTitle: '데이터 차트',     // 모달 제목
  chartLibrary: window.Chart    // Chart.js 라이브러리 (자동)
});</code></pre>
        </div>

        <h5 class="mt-4">메서드</h5>
        <table class="table table-bordered table-striped">
          <thead>
            <tr>
              <th style="width: 280px;">메서드</th>
              <th style="width: 120px;">반환 타입</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>chart.showChart(options)</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>차트 모달 표시</td>
            </tr>
            <tr>
              <td><code>chart.hideChart()</code></td>
              <td><span class="badge bg-secondary">void</span></td>
              <td>차트 모달 숨김</td>
            </tr>
          </tbody>
        </table>

        <h5 class="mt-4">showChart 옵션</h5>
        <table class="table table-bordered table-sm">
          <thead>
            <tr>
              <th style="width: 180px;">옵션</th>
              <th style="width: 100px;">타입</th>
              <th style="width: 150px;">기본값</th>
              <th>설명</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><code>type</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>'bar'</code></td>
              <td>차트 타입 (bar, line, pie, doughnut 등)</td>
            </tr>
            <tr>
              <td><code>title</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>'데이터 차트'</code></td>
              <td>모달 제목</td>
            </tr>
            <tr>
              <td><code>labelField</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>null</code></td>
              <td>X축 레이블 필드명 (groupBy 미지정 시 필수)</td>
            </tr>
            <tr>
              <td><code>dataFields</code></td>
              <td><span class="badge bg-info">Array|String</span></td>
              <td><span class="badge bg-warning">필수</span></td>
              <td>Y축 데이터 필드명 (배열 또는 문자열)</td>
            </tr>
            <tr>
              <td><code>groupBy</code></td>
              <td><span class="badge bg-danger">String</span></td>
              <td><code>null</code></td>
              <td>그룹화 필드명 (지정 시 labelField 무시)</td>
            </tr>
            <tr>
              <td><code>chartOptions</code></td>
              <td><span class="badge bg-info">Object</span></td>
              <td><code>{}</code></td>
              <td>Chart.js 추가 옵션</td>
            </tr>
          </tbody>
        </table>

        <h5 class="mt-4">사용 예제</h5>
        <div class="example-code">
          <pre><code>// 1. 기본 막대 차트 (행별 데이터)
grid.chart.showChart({
  type: 'bar',
  title: '제품별 재고 현황',
  labelField: 'productName',  // X축: 제품명
  dataFields: 'stock'          // Y축: 재고량
});

// 2. 다중 데이터 선형 차트
grid.chart.showChart({
  type: 'line',
  title: '월별 매출/비용 추이',
  labelField: 'month',
  dataFields: ['sales', 'cost']  // 여러 데이터 시리즈
});

// 3. 그룹화 차트 (카테고리별 집계)
grid.chart.showChart({
  type: 'bar',
  title: '카테고리별 수량/금액',
  groupBy: 'category',        // 카테고리로 그룹화
  dataFields: ['quantity', 'amount']
});

// 4. 파이 차트
grid.chart.showChart({
  type: 'pie',
  title: '상태별 분포',
  labelField: 'status',
  dataFields: 'count'
});

// 5. Chart.js 옵션 커스터마이징
grid.chart.showChart({
  type: 'bar',
  labelField: 'month',
  dataFields: 'revenue',
  chartOptions: {
    scales: {
      y: {
        beginAtZero: true,
        ticks: {
          callback: (value) => '₩' + value.toLocaleString()
        }
      }
    },
    plugins: {
      legend: {
        position: 'bottom'
      }
    }
  }
});</code></pre>
        </div>

        <h3 class="mt-5"><i class="bi bi-plugin"></i> 커스텀 플러그인 작성</h3>
        <div class="example-code">
          <pre><code>class MyPlugin extends PluginBase {
  get name() {
    return 'myPlugin';  // 필수: 플러그인 고유 이름
  }

  get version() {
    return '1.0.0';
  }

  install() {
    super.install();
    console.log('MyPlugin 설치됨');
    
    // 그리드 이벤트 리스너 등록
    this.grid.on('afterLoad', this.handleLoad.bind(this));
  }

  uninstall() {
    console.log('MyPlugin 제거됨');
    super.uninstall();
  }

  handleLoad({ data }) {
    this.log(`${data.length}건의 데이터가 로드됨`);
  }

  // 커스텀 메서드
  doSomething() {
    this.grid.showToast('플러그인 동작!', 'success');
  }
}

// 사용
grid.use(MyPlugin);
grid.myPlugin.doSomething();</code></pre>
        </div>
      </div>
    </div>

    <!-- 서버 API 형식 -->
    <h2 class="mt-5">서버 API 형식</h2>
    
    <h4 class="mt-4">데이터 조회 (POST /api/data)</h4>
    <div class="row">
      <div class="col-md-6">
        <h5>요청 (Request)</h5>
        <div class="example-code">
          <pre><code>{
  "page": 1,
  "pageSize": 10,
  "sortOrders": [
    { "field": "name", "order": "asc" }
  ],
  "status": "active",  // queryParams + lastParams
  "category": "food"
}</code></pre>
        </div>
      </div>
      <div class="col-md-6">
        <h5>응답 (Response)</h5>
        <div class="example-code">
          <pre><code>{
  "success": true,
  "rows": [
    { "id": 1, "name": "제품A" },
    { "id": 2, "name": "제품B" }
  ],
  "total": 150
}</code></pre>
        </div>
      </div>
    </div>

    <h4 class="mt-4">데이터 저장 (POST /api/create, /api/update, /api/delete)</h4>
    <div class="row">
      <div class="col-md-6">
        <h5>요청 (Request)</h5>
        <div class="example-code">
          <pre><code>// 추가/수정: 배열 또는 객체
[
  { "name": "신제품", "price": 15000 },
  { "id": 5, "name": "수정제품" }
]

// 삭제: ID 배열
{
  "ids": [1, 2, 3]
}</code></pre>
        </div>
      </div>
      <div class="col-md-6">
        <h5>응답 (Response)</h5>
        <div class="example-code">
          <pre><code>{
  "success": true,
  "inserted": 5,
  "updated": 3,
  "deleted": 2
}</code></pre>
        </div>
      </div>
    </div>

    <!-- 주요 특징 -->
    <h2 class="mt-5">주요 특징</h2>
    <div class="row">
      <div class="col-md-6">
        <ul class="list-group">
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 클라이언트/서버 양쪽 페이징 지원</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 13가지 에디터 타입</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 수식 컬럼 자동 계산</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 인라인 편집 모드</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 엑셀 업로드/다운로드</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 차트 시각화 (Chart.js)</li>
        </ul>
      </div>
      <div class="col-md-6">
        <ul class="list-group">
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 컬럼 리사이징/정렬/숨김</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 유효성 검사 내장</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 이벤트 기반 확장</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 플러그인 시스템</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 반응형 디자인</li>
          <li class="list-group-item"><i class="bi bi-check-circle-fill text-success"></i> 순수 JavaScript (의존성 없음)</li>
        </ul>
      </div>
    </div>

    <!-- 의존성 -->
    <h2 class="mt-5">라이브러리 의존성</h2>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th style="width: 200px;">라이브러리</th>
          <th style="width: 120px;">필수 여부</th>
          <th>용도</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><strong>SmartGrid Core</strong></td>
          <td><span class="badge bg-danger">필수</span></td>
          <td>기본 그리드 기능 (순수 JavaScript)</td>
        </tr>
        <tr>
          <td><strong>XLSX.js</strong></td>
          <td><span class="badge bg-secondary">선택</span></td>
          <td>Excel 플러그인 사용 시 필요</td>
        </tr>
        <tr>
          <td><strong>Chart.js</strong></td>
          <td><span class="badge bg-secondary">선택</span></td>
          <td>Chart 플러그인 사용 시 필요</td>
        </tr>
        <tr>
          <td><strong>Bootstrap Icons</strong></td>
          <td><span class="badge bg-secondary">선택</span></td>
          <td>아이콘 표시 (대체 가능)</td>
        </tr>
      </tbody>
    </table>

    <!-- CDN 링크 -->
    <h2 class="mt-5">CDN 링크</h2>
    <div class="example-code">
      <pre><code>&lt;!-- SmartGrid CSS --&gt;
&lt;link rel="stylesheet" href="path/to/smartgrid.css"&gt;

&lt;!-- SmartGrid JS --&gt;
&lt;script src="path/to/smartgrid.bundle.js"&gt;&lt;/script&gt;

&lt;!-- 선택: XLSX.js (엑셀 기능) --&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"&gt;&lt;/script&gt;

&lt;!-- 선택: Chart.js (차트 기능) --&gt;
&lt;script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"&gt;&lt;/script&gt;

&lt;!-- 선택: Bootstrap Icons --&gt;
&lt;link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.0/font/bootstrap-icons.css"&gt;</code></pre>
    </div>

    <!-- 기본 사용 예제 -->
    <h2 class="mt-5">기본 사용 예제</h2>
    <div class="example-code">
      <pre><code>// 1. HTML
&lt;div id="myTable"&gt;&lt;/div&gt;

// 2. JavaScript
const grid = new SmartGrid('myTable', {
  columns: [
    {
      field: 'id',
      title: 'ID',
      width: '80px',
      hideColumn: true
    },
    {
      field: 'name',
      title: '제품명',
      width: '200px',
      sortable: true,
      editor: {
        type: 'textbox',
        required: true,
        placeholder: '제품명 입력'
      }
    },
    {
      field: 'category',
      title: '카테고리',
      width: '150px',
      editor: {
        type: 'selectbox',
        options: [
          { value: 'food', text: '식품' },
          { value: 'electronics', text: '전자제품' }
        ],
        required: true
      }
    },
    {
      field: 'price',
      title: '가격',
      width: '120px',
      sortable: true,
      sum: true,
      editor: {
        type: 'numberbox',
        decimalPlaces: 0,
        min: 0,
        required: true
      }
    },
    {
      field: 'quantity',
      title: '수량',
      width: '100px',
      editor: {
        type: 'numberbox',
        decimalPlaces: 0,
        defaultVal: 0
      }
    },
    {
      field: 'total',
      title: '합계',
      width: '120px',
      sum: true,
      editor: {
        type: 'numberbox',
        decimalPlaces: 0,
        readonly: true
      },
      formula: (row) => (row.price || 0) * (row.quantity || 0)
    }
  ],
  pageSize: 20,
  pagingMode: 'client', // 또는 'server'
  enableToolbar: true,
  toolbarButtons: ['Add', 'Edit', 'Save', 'Cancel', 'Delete']
});

// 3. 데이터 로드
const data = [
  { id: 1, name: '사과', category: 'food', price: 2000, quantity: 10 },
  { id: 2, name: '노트북', category: 'electronics', price: 1500000, quantity: 2 }
];

await grid.loadData(data);

// 4. 플러그인 사용
grid.use(GridExcelPlugin);
grid.use(GridChartPlugin);

// 5. 이벤트 리스너
grid.on('afterSave', ({ changes }) => {
  console.log('저장 완료:', changes);
});</code></pre>
    </div>

    <footer class="mt-5 pt-4 border-top text-center text-muted">
      <p><strong>SmartGrid</strong> v4.0 - Modern Data Grid Library</p>
      <p>© 2024 SmartGrid. All rights reserved.</p>
    </footer>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
