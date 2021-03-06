=====================
I'mport; REST Client
=====================

Python 사용자를 위한 아임포트 REST API 연동 모듈입니다.

* 이용 중 발생한 문제에 대해 책임지지 않습니다.
* lexifdev님의 도움을 받아 작성되었습니다(`lexifdev's iamport 모듈 <https://github.com/lexifdev/iamport>`_)
* 최초 작성은 `핑크퐁 북스토어 <https://store.pinkfong.com>`_ 에서 쓰기 위해 만들었습니다.

호환성
=======

아직까지 파이썬2만 지원하는 상태입니다. 3 지원은 기여 부탁드립니다.

설치
=======

.. code-block:: shell

    pip install iamport-rest-client


기능
======
1. 결제 정보 찾기
2. 가격 확인
3. 취소



사용법
=======

준비
------

사용하기 위해 객체를 만듭니다.

.. code-block:: python

    from iamport import Iamport

    # 테스트 용
    iamport = Iamport()

    # 실제 상점 정보
    iamport = Iamport(imp_key='{발급받은 키}', imp_secret='{발급받은 시크릿}')



찾기
------

결제를 진행한 상품 아이디나, 전달받은 IMP 아이디를 이용해 결제 정보를 찾습니다.

.. code-block:: python

    # 상품 아이디로 조회
    response = iamport.find(merchant_uid='{상품 아이디}')

    # I'mport; 아이디로 조회
    response = iamport.find(imp_uid='{IMP UID}')


가격 확인
----------

실제 제품 가격과 결제된 가격이 같은지 확인합니다.

.. code-block:: python

    # 상품 아이디로 확인
    iamport.is_paid(product_price, merchant_uid='{상품 아이디}')

    # I'mport; 아이디로 확인
    iamport.is_paid(product_price, imp_uid='{IMP UID}')

    # 이미 찾은 response 재활용하여 확인
    iamport.is_paid(product_price, response=response)


취소
------

결제를 취소합니다.

.. code-block:: python

    # 상품 아이디로 취소
    response = iamport.cancel(u'취소하는 이유', merchant_uid='{상품 아이디}')

    # I'mport; 아이디로 취소
    response = iamport.cancel(u'취소하는 이유', imp_uid='{IMP UID}')

    # 취소시 오류 예외처리(이미 취소된 결제는 에러가 발생함)
    try:
        response = iamport.cancel(u'취소하는 이유', imp_uid='{IMP UID}')
    except Iamport.ResonseError as e:
        print e.code
        print e.message  # 에러난 이유를 알 수 있음


할 일
======
- 파이썬 3 지원
- 결제 목록 읽기
- 비 인증 결제 지원
- 테스트
- 문서화
- 기타 등등
