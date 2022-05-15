```
직전 트러블슈팅에 이어서)
3-1. problem: 모달영역 스크롤 후 닫기 버튼 클릭하면 모달 탑 영역이 보인 후 사라짐.
     컴포넌트가 새로 렌더링되며 탑 영역이 보이는 것.
     텍스트 영역을 child component로 분리해 React.memo로 감싸주어도 parent가 리렌더링되면 탑 영역이 보임.
3-2. to solve: 모달 닫기 버튼 눌렀을 때 모달T의 스크롤 y값을 가져와 모달F에 적용
     making refs for : show true modal, show false modal, scroll y value in show true modal
     when clicking the modal closing button, get scrollTop for modalT before changing show state
     useLayoutEffect good! useEffect is not good for this time.
      : useLayoutEffect works after layout while useEffect works after layout and paint
     scrollTop for modalF is set, then modalF is painted
```
```
function DescModal({
  modalScrollY,
  modalFRef,
  modalTRef,
  isShowOn,
  desc,
}: {
  modalScrollY: React.MutableRefObject<number>;
  modalFRef: React.RefObject<HTMLDivElement>;
  modalTRef: React.RefObject<HTMLDivElement>;
  isShowOn: boolean;
  desc: string;
}) {
  // 모달F가 화면에 그려지기 전 스크롤Y 설정
  useLayoutEffect(() => {
    modalFRef.current?.scroll(0, modalScrollY.current);
  }, [isShowOn]);

  if (isShowOn) {
    return <ModalContainerT ref={modalTRef}>{desc}</ModalContainerT>;
  }
  return <ModalContainerF ref={modalFRef}>{desc}</ModalContainerF>;
  ```
  
  ```
  
function NovelColumnDetail({ novel }: MyComponentProps) {
                    .
                    .
                    .
  // (문제)모달 스크롤을 내린 후 모달을 닫으면 모달 탑 영역이 보이고 사라짐
  // (대처)닫기 버튼을 누른 직후 모달T의 스크롤y 값을 가져와 모달F에 적용
  const modalTRef = useRef<HTMLDivElement>(null);
  const modalFRef = useRef<HTMLDivElement>(null);
  const modalScrollY = useRef(0);

  const getModalScroll = () => {
    modalScrollY.current = modalTRef.current?.scrollTop as number;
  };

  return (
                    .
                    .                            

              {isModal && (
                <DownIconBox
                  onClick={() => {
                    getModalScroll();
                    handleModal();
                  }}
                >
                  <DownIcon />
                </DownIconBox>
              )}
              {!isModal && (
                <UpIconBox>
                  <UpIcon onClick={handleModal} />
                </UpIconBox>
              )}
                    .
                    . 
          {isModal && (
            <DescModal
              modalScrollY={modalScrollY}
              modalTRef={modalTRef}
              modalFRef={modalFRef}
              isShowOn={isShowModal}
              desc={desc}
            />
          )}

                    .
                    .

```
```
필요한 것만 빼고 지우니까 코드가 휑하네ㅎㅎ
악 피곤하다. 그래도 어떻게든 해결했다ㅎㅎ
영어로 쓰는 연습해 봤는데 시간 오래 걸림. 지치고 졸린 나는 한국어로 쓰겠음..
바이바이..
```
-22.03.15-
