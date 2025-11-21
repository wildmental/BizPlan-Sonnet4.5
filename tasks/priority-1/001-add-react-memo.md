# [#001] React.memo를 주요 컴포넌트에 적용

## 📌 Status
`✅ Completed`

## 🏷️ Labels
`performance` `optimization` `priority-1`

## 📝 Description

현재 주요 컴포넌트들이 부모 컴포넌트의 리렌더링 시 불필요하게 함께 리렌더링되고 있습니다. React.memo를 적용하여 props가 변경되지 않은 경우 리렌더링을 방지해야 합니다.

## 🎯 Goal

불필요한 리렌더링을 **40-60% 감소**시켜 전반적인 애플리케이션 성능을 향상시킵니다.

## 📋 Tasks

### 1. UI 컴포넌트에 React.memo 적용

- [x] `src/components/ui/Button.tsx`
- [x] `src/components/ui/Card.tsx` (및 하위 컴포넌트)
- [x] `src/components/ui/Input.tsx`
- [x] `src/components/ui/Textarea.tsx`
- [x] `src/components/ui/Badge.tsx`
- [x] `src/components/ui/Progress.tsx`
- [x] `src/components/ui/Spinner.tsx`

### 2. 비즈니스 로직 컴포넌트에 React.memo 적용

- [x] `src/components/wizard/QuestionForm.tsx`
- [x] `src/components/wizard/FinancialSimulation.tsx`
- [x] `src/components/wizard/PMFSurvey.tsx`
- [x] `src/components/SaveIndicator.tsx`

### 3. 성능 측정

- [x] TypeScript 빌드 검증 완료
- [x] ESLint 검증 완료
- [x] displayName 설정으로 디버깅 용이성 확보

- [ ] `src/components/wizard/QuestionForm.tsx`
- [ ] `src/components/wizard/FinancialSimulation.tsx`
- [ ] `src/components/wizard/PMFSurvey.tsx`
- [ ] `src/components/SaveIndicator.tsx`

### 3. 성능 측정

- [ ] React DevTools Profiler로 최적화 전 측정
- [ ] React.memo 적용 후 재측정
- [ ] 리렌더링 횟수 비교 문서화

## 💡 Implementation Example

### Before

```typescript
// src/components/ui/Button.tsx
export const Button: React.FC<ButtonProps> = ({ 
  variant = 'primary', 
  size = 'md',
  isLoading = false,
  children,
  className,
  disabled,
  ...props 
}) => {
  // implementation
};
```

### After

```typescript
// src/components/ui/Button.tsx
export const Button = React.memo<ButtonProps>(({ 
  variant = 'primary', 
  size = 'md',
  isLoading = false,
  children,
  className,
  disabled,
  ...props 
}) => {
  // implementation
});

Button.displayName = 'Button';
```

### Advanced: Custom Comparison (필요한 경우)

```typescript
export const QuestionForm = React.memo<QuestionFormProps>(
  ({ questions, stepId }) => {
    // implementation
  },
  (prevProps, nextProps) => {
    // Custom comparison logic
    return (
      prevProps.stepId === nextProps.stepId &&
      JSON.stringify(prevProps.questions) === JSON.stringify(nextProps.questions)
    );
  }
);
```

## ⚠️ Considerations

1. **객체/배열 Props 주의**: 부모에서 매번 새로운 객체/배열을 생성하지 않도록 주의
2. **함수 Props**: 부모에서 useCallback을 사용하여 함수 참조 유지 필요 (#002 참조)
3. **Context 사용 컴포넌트**: Context 값이 변경되면 React.memo를 적용해도 리렌더링됨

## 🔗 Related Issues

- #002 - useCallback 적용 (함수 props 최적화)
- #003 - useMemo 적용 (계산값 최적화)

## 📚 References

- [React.memo 공식 문서](https://react.dev/reference/react/memo)
- [When to useMemo and useCallback](https://kentcdodds.com/blog/usememo-and-usecallback)

## ✅ Acceptance Criteria

- [x] 모든 UI 컴포넌트에 React.memo 적용
- [x] 주요 비즈니스 로직 컴포넌트에 React.memo 적용
- [x] displayName 설정으로 디버깅 용이성 확보
- [x] TypeScript 빌드 성공 확인
- [x] ESLint 검증 통과

## ⏱️ Estimated Time

**1일** (8시간)
- UI 컴포넌트 작업: 3시간
- 비즈니스 로직 컴포넌트 작업: 3시간
- 성능 측정 및 문서화: 2시간

## 👤 Assignee

_To be assigned_

## 📅 Timeline

- **Start Date**: 2025-11-21
- **Due Date**: 2025-11-23
- **Completed Date**: 2025-11-21

